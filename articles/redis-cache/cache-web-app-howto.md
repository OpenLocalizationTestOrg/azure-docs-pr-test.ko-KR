---
title: "Redis Cache에 웹 앱 aaaHow toocreate | Microsoft Docs"
description: "자세한 내용은 방법 toocreate Redis Cache에 웹 앱"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="e51d5-103">어떻게 toocreate Redis Cache에 웹 앱</span><span class="sxs-lookup"><span data-stu-id="e51d5-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e51d5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="e51d5-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="e51d5-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e51d5-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="e51d5-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="e51d5-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="e51d5-107">Java</span><span class="sxs-lookup"><span data-stu-id="e51d5-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="e51d5-108">Python</span><span class="sxs-lookup"><span data-stu-id="e51d5-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="e51d5-109">이 자습서에서는 어떻게 toocreate Visual Studio 2017을 사용 하 여 Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램 tooa 웹 앱 및 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="e51d5-110">hello 샘플 응용 프로그램 데이터베이스의 통계를 팀의 목록을 표시 하 고 다양 한 방법 toouse Azure Redis Cache toostore 보여주며, hello 캐시에서 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="e51d5-111">Hello 자습서를 완료 하면 실행 중인 웹 응용 프로그램이 Azure에서 읽고 tooa 데이터베이스, Azure Redis Cache로 최적화 하 고 호스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="e51d5-112">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-112">You'll learn:</span></span>

* <span data-ttu-id="e51d5-113">어떻게 toocreate ASP.NET MVC 5는 Visual Studio에서 응용 프로그램 웹입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="e51d5-114">어떻게 tooaccess 데이터베이스의에서 데이터를 Entity Framework를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="e51d5-115">어떻게 tooimprove 데이터 처리량 하 고 저장 하 고 Azure Redis Cache를 사용 하 여 데이터를 검색 하 여 데이터베이스 로드를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="e51d5-116">Redis toouse 집합 tooretrieve hello 상위 5 팀 정렬 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="e51d5-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="e51d5-117">어떻게 tooprovision hello 리소스 관리자 템플릿을 사용 하 여 hello 응용 프로그램에 대 한 Azure 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="e51d5-118">어떻게 toopublish Visual Studio를 사용 하 여 응용 프로그램 tooAzure hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e51d5-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e51d5-119">Prerequisites</span></span>
<span data-ttu-id="e51d5-120">toocomplete hello 자습서 hello 다음 필수 구성 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="e51d5-121">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="e51d5-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="e51d5-122">Azure SDK for.NET hello로 visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e51d5-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="e51d5-123">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="e51d5-123">Azure account</span></span>
<span data-ttu-id="e51d5-124">Azure 계정 toocomplete hello 자습서가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="e51d5-125">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-125">You can:</span></span>

* <span data-ttu-id="e51d5-126">[Azure 계정을 무료로 개설할 수 있습니다](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="e51d5-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="e51d5-127">Azure 서비스를 유료 아웃 사용된 tootry 일 수 있는 크레딧을 얻게.</span><span class="sxs-lookup"><span data-stu-id="e51d5-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="e51d5-128">Hello 크레딧을 모두 사용 된 후에 hello 계정을 유지 하 고 무료 Azure 서비스 및 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="e51d5-129">[Visual Studio 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero)</span><span class="sxs-lookup"><span data-stu-id="e51d5-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="e51d5-130">MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="e51d5-131">Azure SDK for.NET hello로 visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e51d5-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="e51d5-132">hello 자습서 용으로 작성 된 Visual Studio 2017 hello로 [Azure SDK for.NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="e51d5-133">Azure SDK 2.9.5 hello hello Visual Studio 설치 관리자 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="e51d5-134">Visual Studio 2015를가지고 있는 경우 참고할 수 hello로 hello 자습서 [Azure SDK for.NET](../dotnet-sdk.md) 2.8.2 이상.</span><span class="sxs-lookup"><span data-stu-id="e51d5-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="e51d5-135">[다운로드 Visual Studio 2015 용 여기 최신 Azure SDK을 hello](http://go.microsoft.com/fwlink/?linkid=518003)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="e51d5-136">Visual Studio는 아직 없는 경우 hello SDK로 자동으로 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="e51d5-137">일부 화면이이 자습서의 예제는 hello 나오는 그림에서 다르게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="e51d5-138">Visual Studio 2013를 설정한 경우 다음을 할 수 있습니다 [다운로드 Visual Studio 2013 용 최신 Azure SDK hello](http://go.microsoft.com/fwlink/?LinkID=324322)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="e51d5-139">일부 화면이이 자습서의 예제는 hello 나오는 그림에서 다르게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="e51d5-140">Hello Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="e51d5-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="e51d5-141">Visual Studio를 열고 **파일**, **새로 만들기**, **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="e51d5-142">Hello 확장 **Visual C#** hello에 대 한 노드 **템플릿** 목록에서 **클라우드**를 클릭 하 고 **ASP.NET 웹 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="e51d5-143">**.NET Framework 4.5.2** 이상이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="e51d5-144">형식 **ContosoTeamStats** hello에 **이름** 텍스트 상자를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![프로젝트 만들기][cache-create-project]
3. <span data-ttu-id="e51d5-146">선택 **MVC** hello 프로젝트 형식을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="e51d5-147">되도록 **인증 안 함** hello에 대 한 지정 된 **인증** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="e51d5-148">Visual Studio의 버전을 따라 hello 기본 toosomething 다른 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="e51d5-149">toochange, 클릭 **인증 변경** 선택 **인증 안 함**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="e51d5-150">Hello의 선택을 취소 하는 경우 Visual Studio 2015와 함께, **hello 클라우드의 호스트에에서** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="e51d5-151">살펴볼 [프로 비전 hello Azure 리소스](#provision-the-azure-resources) 및 [hello 응용 프로그램 tooAzure 게시](#publish-the-application-to-azure) hello 자습서의 이후 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="e51d5-152">그대로 유지 되므로 Visual Studio에서 앱 서비스 웹 응용 프로그램을 프로 비전에 대 한 예제 **hello 클라우드의 호스트에에서** 참조 옵션을 선택 [Azure 앱 서비스에서 ASP.NET 및 Visual Studio를 사용 하 여 웹 응용 프로그램 시작](../app-service-web/app-service-web-get-started-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![프로젝트 템플릿 선택][cache-select-template]
4. <span data-ttu-id="e51d5-154">클릭 **확인** toocreate hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="e51d5-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="e51d5-155">Hello ASP.NET MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e51d5-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="e51d5-156">Hello 자습서의이 섹션에서는 데이터베이스에서 팀 통계를 표시 하는 hello 기본 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="e51d5-157">Hello Entity Framework NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="e51d5-158">Hello 모델 추가</span><span class="sxs-lookup"><span data-stu-id="e51d5-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="e51d5-159">Hello 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="e51d5-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="e51d5-160">Hello 보기 구성</span><span class="sxs-lookup"><span data-stu-id="e51d5-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="e51d5-161">Hello Entity Framework NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="e51d5-162">클릭 **NuGet 패키지 관리자**, **패키지 관리자 콘솔** hello에서 **도구** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="e51d5-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="e51d5-163">실행 hello 다음 hello에서 명령을 **패키지 관리자 콘솔** 창.</span><span class="sxs-lookup"><span data-stu-id="e51d5-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="e51d5-164">이 패키지에 대 한 자세한 내용은 참조 hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet 페이지.</span><span class="sxs-lookup"><span data-stu-id="e51d5-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="e51d5-165">Hello 모델 추가</span><span class="sxs-lookup"><span data-stu-id="e51d5-165">Add hello model</span></span>
1. <span data-ttu-id="e51d5-166">**솔루션 탐색기**에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![모델 추가][cache-model-add-class]
2. <span data-ttu-id="e51d5-168">입력 `Team` hello 클래스 이름 및 클릭에 대 한 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![모델 클래스 추가][cache-model-add-class-dialog]
3. <span data-ttu-id="e51d5-170">Hello 대체 `using` hello 위쪽 hello에 문을 `Team.cs` hello 다음과 같이 파일 `using` 문.</span><span class="sxs-lookup"><span data-stu-id="e51d5-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="e51d5-171">Hello의 hello 정의 바꿉니다 `Team` 다음 업데이트 된 포함 된 코드 조각 hello 사용 하 여 클래스 `Team` 클래스 정의 뿐만 아니라 다른 Entity Framework 도우미 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="e51d5-172">Hello 코드 첫 번째 접근 방식 tooEntity이이 자습서에 사용 되는 프레임 워크에 대 한 자세한 내용은 참조 하십시오. [코드 첫 번째 tooa 새 데이터베이스](https://msdn.microsoft.com/data/jj193542)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. <span data-ttu-id="e51d5-173">**솔루션 탐색기**를 두 번 클릭 **web.config** tooopen 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="e51d5-175">Hello 다음 추가 `connectionStrings` 섹션.</span><span class="sxs-lookup"><span data-stu-id="e51d5-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="e51d5-176">hello 연결 문자열의 이름으로 hello hello는 Entity Framework 데이터베이스 컨텍스트 클래스의 hello 이름과 같아야 합니다. `TeamContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="e51d5-177">새 hello를 추가할 수 있습니다 `connectionStrings` 섹션 뒤에 오도록 `configSections`hello 다음 예제에에서 나온 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > <span data-ttu-id="e51d5-178">연결 문자열에는 Visual Studio의 hello 버전에 따라 다를 수 있습니다 및 SQL Server Express edition toocomplete hello 자습서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="e51d5-179">hello web.config 템플릿을 설치, 구성 된 toomatch 여야 하며 포함 될 수 있습니다 `Data Source` 항목 같은 `(LocalDB)\v11.0` (SQL Server Express 2012)에서 또는 `Data Source=(LocalDB)\MSSQLLocalDB` (SQL Server Express 2014에서 이상 버전).</span><span class="sxs-lookup"><span data-stu-id="e51d5-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="e51d5-180">연결 문자열 및 SQL Express 버전에 대한 자세한 내용은 [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e51d5-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="e51d5-181">Hello 컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="e51d5-181">Add hello controller</span></span>
1. <span data-ttu-id="e51d5-182">키를 눌러 **F6** toobuild hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="e51d5-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="e51d5-183">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **컨트롤러** 폴더 선택 **추가**, **컨트롤러**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![컨트롤러 추가][cache-add-controller]
3. <span data-ttu-id="e51d5-185">**Entity Framework를 사용하여 보기가 포함된 MVC 5 컨트롤러**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="e51d5-186">클릭 한 후 오류가 발생 하는 경우 **추가**, hello 프로젝트를 먼저 작성 한을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![컨트롤러 클래스 추가][cache-add-controller-class]
4. <span data-ttu-id="e51d5-188">선택 **팀 (ContosoTeamStats.Models)** hello에서 **모델 클래스** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="e51d5-189">선택 **TeamContext (ContosoTeamStats.Models)** hello에서 **데이터 컨텍스트 클래스가** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="e51d5-190">형식 `TeamsController` hello에 **컨트롤러** 이름 텍스트 상자 (것 채워지지 않는 경우 자동으로).</span><span class="sxs-lookup"><span data-stu-id="e51d5-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="e51d5-191">클릭 **추가** toocreate 컨트롤러 클래스 hello 및 hello 기본 보기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![컨트롤러 구성][cache-configure-controller]
5. <span data-ttu-id="e51d5-193">**솔루션 탐색기**를 확장 하 고 **Global.asax** 두 번 클릭 하 고 **Global.asax.cs** tooopen 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="e51d5-195">Hello 다음 두 개의 추가 `using` hello hello 다른 파일의 hello 위쪽에서 문을 `using` 문.</span><span class="sxs-lookup"><span data-stu-id="e51d5-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="e51d5-196">다음 코드의 hello hello 끝에 줄을 hello 추가 `Application_Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e51d5-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="e51d5-197">**솔루션 탐색기**에서 `App_Start`를 확장하고 `RouteConfig.cs`를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="e51d5-199">대체 `controller = "Home"` hello hello에서 코드 다음에 `RegisterRoutes` 메서드 `controller = "Teams"` hello 다음 예제와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="e51d5-200">Hello 보기 구성</span><span class="sxs-lookup"><span data-stu-id="e51d5-200">Configure hello views</span></span>
1. <span data-ttu-id="e51d5-201">**솔루션 탐색기**, hello 확장 **뷰** 폴더를 선택한 다음 hello **Shared** 폴더를 찾아 두 번 클릭 **_Layout.cshtml**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="e51d5-203">Hello의 hello 내용을 변경 `title` 요소 및 바꾸기 `My ASP.NET Application` 와 `Contoso Team Stats` hello 다음 예제와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="e51d5-204">Hello에 `body` 섹션에서 hello를 먼저 업데이트 `Html.ActionLink` 문과 바꾸기 `Application name` 와 `Contoso Team Stats` 바꾸고 `Home` 와 `Teams`합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="e51d5-205">이전: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="e51d5-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="e51d5-206">이후: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="e51d5-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![코드 변경 내용][cache-layout-cshtml-code]
2. <span data-ttu-id="e51d5-208">키를 눌러 **Ctrl + f 5** hello 응용 프로그램 toobuild 및 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="e51d5-209">이 버전의 hello 응용 프로그램 hello 데이터베이스에서 직접 hello 결과 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="e51d5-210">참고 hello **새로 만들기**, **편집**, **세부 정보**, 및 **삭제** 자동으로 된 동작은 hello 여 toohello 응용 프로그램을 추가 **Entity Framework를 사용 하 여 뷰를 포함 된 MVC 5 컨트롤러** 스 캐 폴드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="e51d5-211">Hello hello 자습서의 다음 섹션에서 Redis Cache toooptimize hello 데이터 액세스 및 추가 기능을 제공 toohello 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![시작 응용 프로그램][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="e51d5-213">Hello 응용 프로그램 toouse Redis 캐시 구성</span><span class="sxs-lookup"><span data-stu-id="e51d5-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="e51d5-214">Hello 자습서의이 섹션에서는 샘플 응용 프로그램 toostore hello 구성 및 Azure Redis Cache 인스턴스에서 hello를 사용 하 여 Contoso 팀 통계를 검색 합니다 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) 캐시 클라이언트입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="e51d5-215">Hello 응용 프로그램 toouse StackExchange.Redis 구성</span><span class="sxs-lookup"><span data-stu-id="e51d5-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="e51d5-216">Hello TeamsController 클래스 tooreturn 결과 hello 캐시 또는 hello 데이터베이스에서 업데이트</span><span class="sxs-lookup"><span data-stu-id="e51d5-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="e51d5-217">Hello 만들기, 편집, 업데이트 및 삭제 작업 hello 캐시와 toowork 메서드</span><span class="sxs-lookup"><span data-stu-id="e51d5-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="e51d5-218">Hello 팀 인덱스 뷰 toowork hello 캐시 업데이트</span><span class="sxs-lookup"><span data-stu-id="e51d5-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="e51d5-219">Hello 응용 프로그램 toouse StackExchange.Redis 구성</span><span class="sxs-lookup"><span data-stu-id="e51d5-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="e51d5-220">tooconfigure hello StackExchange.Redis NuGet 패키지를 사용 하 여 Visual Studio에서 클라이언트 응용 프로그램 클릭 **NuGet 패키지 관리자**, **패키지 관리자 콘솔** hello에서 **도구** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="e51d5-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="e51d5-221">실행 hello 다음 hello에서 명령을 `Package Manager Console` 창.</span><span class="sxs-lookup"><span data-stu-id="e51d5-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="e51d5-222">NuGet 패키지가 다운로드 되 고 추가 하는 hello hello hello StackExchange.Redis 캐시 클라이언트를 사용한 프로그램 클라이언트 응용 프로그램 tooaccess Azure Redis Cache에 대 한 어셈블리 참조가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="e51d5-223">강력한 이름의 버전의 hello toouse 것을 선호 하는 경우 `StackExchange.Redis` 클라이언트 라이브러리, 설치 hello `StackExchange.Redis.StrongName` 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="e51d5-224">**솔루션 탐색기**, hello 확장 **컨트롤러** 폴더를 두 번 클릭 **TeamsController.cs** tooopen 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![팀 컨트롤러][cache-teamscontroller]
4. <span data-ttu-id="e51d5-226">다음 두 개의 hello 추가 `using` 문을 너무**TeamsController.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="e51d5-227">다음 두 개의 속성 toohello hello 추가 `TeamsController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-227">Add hello following two properties toohello `TeamsController` class.</span></span>

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. <span data-ttu-id="e51d5-228">라는 컴퓨터에서 파일을 만들 `WebAppPlusCacheAppSecrets.config` toocheck 결정 해야 샘플 응용 프로그램의 hello 소스 코드를 사용 하 여 체크지 않습니다 하는 위치에 배치 위치에서.</span><span class="sxs-lookup"><span data-stu-id="e51d5-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="e51d5-229">이 예제에서는 hello에 `AppSettingsSecrets.config` 파일은 `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="e51d5-230">Hello 편집 `WebAppPlusCacheAppSecrets.config` 파일을 hello 다음 내용을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="e51d5-231">Hello 응용 프로그램을 로컬로 실행 하는 경우이 정보는 사용 되는 tooconnect tooyour Azure Redis Cache 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="e51d5-232">Hello 자습서의 뒷부분에 나오는 Azure Redis 캐시 인스턴스를 프로 비전 하 고 hello 캐시 이름 및 암호를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="e51d5-233">Toorun hello 샘플 응용 프로그램 않을 계획 이라면 로컬로이 파일의 hello 만들기를 건너뛸 수 있습니다 및 tooAzure hello 응용 프로그램을 배포 하는 경우 때문에 hello 파일을 참조 하는 hello 후속 단계 hello 응용 프로그램에서 연결 정보를 캐시 하는 hello 검색 이 파일에서가 아니라 및 hello 웹 앱에 대 한 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="e51d5-234">Hello 이후 `WebAppPlusCacheAppSecrets.config` 배포 되지 않은 응용 프로그램과 함께 tooAzure, 필요 없는 toorun hello 응용 프로그램을 로컬 하려는 경우가 아니면 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="e51d5-235">**솔루션 탐색기**를 두 번 클릭 **web.config** tooopen 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="e51d5-237">Hello 다음 추가 `file` toohello 특성 `appSettings` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="e51d5-238">다른 파일 이름 또는 위치를 사용 하는 경우 hello 예제에 표시 된 것과 hello에 대 한 해당 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="e51d5-239">이전: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="e51d5-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="e51d5-240">이후: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="e51d5-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="e51d5-241">hello에서 hello 태그와 hello 외부 파일의 hello 내용을 병합 하는 hello ASP.NET 런타임 `<appSettings>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="e51d5-242">hello 형식의 hello 지정 된 파일을 찾을 수 없는 경우 hello 파일 특성을 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="e51d5-243">비밀 내용 (연결 문자열 tooyour 캐시 hello) hello 응용 프로그램에 대 한 hello 소스 코드의 일부분으로 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="e51d5-244">웹 앱 tooAzure를 배포할 때 hello `WebAppPlusCacheAppSecrests.config` (즉, 대상) 파일을 배포 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="e51d5-245">여러 가지 방법으로 toospecify 이러한 암호 Azure이 고이 자습서에서 사용 하도록 구성 된 자동으로 있습니다 때 있습니다 [프로 비전 할 Azure 리소스 hello](#provision-the-azure-resources) 이후 자습서 단계에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="e51d5-246">Azure에서 암호 사용에 대 한 자세한 내용은 참조 [암호 및 기타 중요 한 데이터 tooASP.NET 및 Azure 앱 서비스 배포에 대 한 유용한](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="e51d5-247">Hello TeamsController 클래스 tooreturn 결과 hello 캐시 또는 hello 데이터베이스에서 업데이트</span><span class="sxs-lookup"><span data-stu-id="e51d5-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="e51d5-248">이 샘플에서는 팀 통계 또는 hello 캐시 hello 데이터베이스에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="e51d5-249">팀 통계로 직렬화 된 hello 캐시에 저장 된 `List<Team>`, Redis 데이터 형식을 사용 하 여 정렬 된 집합으로도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="e51d5-250">정렬된 집합에서 항목을 검색하는 경우 일부 또는 모두 검색하거나 특정 항목을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="e51d5-251">이 샘플에서 hello 상위 5 개 팀을 기준으로 wins의 수에 대 한 hello 정렬 된 집합을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="e51d5-252">순서 toouse Azure Redis Cache에에서 hello 캐시의 여러 형식에 필요한 toostore hello 팀 통계는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="e51d5-253">이 자습서에서는 여러 개의 형식 toodemonstrate 일부 hello 다양 한 방법 및 다른 데이터 형식의 toocache 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="e51d5-254">Hello 다음 추가 `using` 문 toohello `TeamsController.cs` 다른 hello로 hello 위쪽 파일 `using` 문.</span><span class="sxs-lookup"><span data-stu-id="e51d5-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="e51d5-255">Hello 현재 대체 `public ActionResult Index()` 구현을 다음 hello로 메서드를 구현 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="e51d5-256">다음 세 가지 메서드 toohello hello 추가 `TeamsController` 클래스 tooimplement hello `playGames`, `clearCache`, 및 `rebuildDB` hello에서 동작 유형에 switch 문 hello 이전 코드 조각에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="e51d5-257">hello `PlayGames` 의 게임 시즌 시뮬레이션 하 여 hello 팀 통계를 업데이트 하는 메서드, 저장 결과 toohello 데이터베이스 hello 및 지웁니다 hello hello 캐시에서 데이터에 이제 오래 된 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="e51d5-258">hello `RebuildDB` 메서드 다시 초기화 hello hello 기본 설정 된 데이터베이스를 팀,에 대 한 통계를 생성 하 고 지웁니다 hello hello 캐시에서 데이터에 이제 오래 된 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="e51d5-259">hello `ClearCachedTeams` 메서드 hello 캐시에서 모든 캐시 된 팀 통계를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="e51d5-260">다음 네 가지 메서드가 toohello hello 추가 `TeamsController` 클래스 tooimplement hello hello 캐시 및 hello 데이터베이스에서 hello 팀 통계를 검색 하는 다양 한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="e51d5-261">이러한 각 방법의 반환을 `List<Team>` hello 보기 하 여 다음 표시 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="e51d5-262">hello `GetFromDB` 메서드 hello 데이터베이스에서 hello 팀 통계를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    <span data-ttu-id="e51d5-263">hello `GetFromList` 메서드는 serialize 된으로 캐시에서 hello 팀 통계를 읽기 `List<Team>`합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="e51d5-264">캐시 누락 이면 hello 팀 통계 hello 데이터베이스에서 읽은 업데이트 하 고에 hello 캐시에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="e51d5-265">이 샘플에서 JSON.NET serialization tooserialize hello.NET 개체 tooand hello 캐시에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="e51d5-266">자세한 내용은 참조 [toowork.NET과 함께 Azure Redis Cache에서 개체를 어떻게](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="e51d5-267">hello `GetFromSortedSet` 메서드는 캐시 된 정렬 된 집합에서 hello 팀 통계를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="e51d5-268">캐시 누락 이면 hello 팀 통계 hello 데이터베이스에서 읽은 업데이트 하 고 정렬 된 집합으로 hello 캐시에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="e51d5-269">hello `GetFromSortedSetTop5` 메서드 hello 상위 정렬 hello 캐시에서 5 팀 집합을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="e51d5-270">Hello 캐시 hello hello 있는지 여부를 확인 하 여 시작 `teamsSortedSet` 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="e51d5-271">이 키가 있는 경우 hello `GetFromSortedSet` 메서드 tooread hello 팀 통계 라 하 고 hello 캐시에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="e51d5-272">다음으로 hello 캐시 된 정렬 된 집합이 쿼리 하는 hello 상위 5 팀 반환 되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="e51d5-273">Hello 만들기, 편집, 업데이트 및 삭제 작업 hello 캐시와 toowork 메서드</span><span class="sxs-lookup"><span data-stu-id="e51d5-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="e51d5-274">hello 스 캐 폴딩 생성 된 코드는이 샘플의 일부 메서드 tooadd 포함 되는 편집 및 팀을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="e51d5-275">팀 추가, 편집 또는 제거할 때마다 hello 캐시의 hello 데이터가 오래 됨.</span><span class="sxs-lookup"><span data-stu-id="e51d5-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="e51d5-276">수정 하면서 간단한이 섹션에서는 이러한 세 가지 방법 tooclear hello 팀 캐시에 저장 되어 hello 캐시 hello 데이터베이스와 동기화 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="e51d5-277">Toohello 찾아보기 `Create(Team team)` hello에 대 한 메서드 `TeamsController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="e51d5-278">호출 toohello 추가 `ClearCachedTeams` 메서드를 다음 예제는 hello와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="e51d5-279">Toohello 찾아보기 `Edit(Team team)` hello에 대 한 메서드 `TeamsController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="e51d5-280">호출 toohello 추가 `ClearCachedTeams` 메서드를 다음 예제는 hello와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="e51d5-281">Toohello 찾아보기 `DeleteConfirmed(int id)` hello에 대 한 메서드 `TeamsController` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="e51d5-282">호출 toohello 추가 `ClearCachedTeams` 메서드를 다음 예제는 hello와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="e51d5-283">Hello 팀 인덱스 뷰 toowork hello 캐시 업데이트</span><span class="sxs-lookup"><span data-stu-id="e51d5-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="e51d5-284">**솔루션 탐색기**, hello 확장 **뷰** hello 후 폴더를 **팀** 폴더를 찾아 두 번 클릭 **Index.cshtml**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="e51d5-286">Hello 파일의 hello 위쪽 단락 요소 다음에 오는 hello를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![작업 테이블][cache-teams-index-table]
   
    <span data-ttu-id="e51d5-288">이 hello 링크 toocreate 새 팀입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="e51d5-289">다음 표에 hello hello 단락 요소를 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="e51d5-290">이 테이블에는 게임, hello 캐시를 지워 새 시즌 재생 하는 새 팀을 만들기 위한 작업 링크, 다른 여러 형식으로 hello 캐시에서 hello 팀 검색, hello 팀 hello 데이터베이스에서 검색 및 다시 작성 hello 새 예제 데이터를 사용 하 여 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. <span data-ttu-id="e51d5-291">Hello toohello 맨 아래로 스크롤 **Index.cshtml** 파일을 hello 다음 추가 `tr` 요소 hello 마지막 행 hello에 있도록 마지막 테이블에 hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="e51d5-292">이 행의 hello 값을 표시 `ViewBag.Msg` hello 현재 작업에 대 한 상태 보고서를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="e51d5-293">hello `ViewBag.Msg` hello 이전 단계의 hello 작업 링크 중 하나를 클릭할 때 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![상태 메시지][cache-status-message]
2. <span data-ttu-id="e51d5-295">키를 눌러 **F6** toobuild hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="e51d5-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="e51d5-296">프로 비전 hello Azure 리소스</span><span class="sxs-lookup"><span data-stu-id="e51d5-296">Provision hello Azure resources</span></span>
<span data-ttu-id="e51d5-297">toohost Azure에서 응용 프로그램을 먼저 프로 비전 해야 hello 응용 프로그램에 필요한 Azure 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="e51d5-298">이 자습서에서는 샘플 응용 프로그램 hello Azure 서비스를 수행 하는 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="e51d5-299">Azure Redis 캐시(영문)</span><span class="sxs-lookup"><span data-stu-id="e51d5-299">Azure Redis Cache</span></span>
* <span data-ttu-id="e51d5-300">앱 서비스 웹앱</span><span class="sxs-lookup"><span data-stu-id="e51d5-300">App Service Web App</span></span>
* <span data-ttu-id="e51d5-301">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="e51d5-301">SQL Database</span></span>

<span data-ttu-id="e51d5-302">toodeploy 이러한 서비스 tooa 기존 또는 새 리소스 그룹을 선택한 다음 hello 클릭 **tooAzure 배포** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="e51d5-303">[! [TooAzure deploy] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e51d5-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="e51d5-304">이 **tooAzure 배포** 단추 hello를 사용 하 여 [웹 응용 프로그램와 Redis Cache, SQL 데이터베이스를 만들](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure 빠른 시작](https://github.com/Azure/azure-quickstart-templates) 템플릿 tooprovision 이러한 서비스와 집합 hello Azure Redis Cache 연결 문자열 hello에 대 한 hello hello 및 SQL 데이터베이스 응용 프로그램 설정에 대 한 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="e51d5-305">Azure 계정이 없는 경우 몇 분 만에 [무료 계정을 만들](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="e51d5-306">클릭 하 여 hello **tooAzure 배포** 단추 toohello Azure 포털 사용 및 시작 hello hello 서식 파일에서 설명 하는 hello 리소스를 만드는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![TooAzure 배포][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="e51d5-308">Hello에 **기본 사항** 섹션 hello Azure 구독 toouse 하 고 기존 리소스 그룹을 선택 하거나 새 대시보드를 만든 선택한 hello 리소스 그룹 위치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="e51d5-309">Hello에 **설정** 섹션에서 지정 된 **관리자 로그인** (사용 하지 마십시오 **관리자**), **관리자 로그인 암호**, 및  **데이터베이스 이름**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="e51d5-310">hello 다른 매개 변수가 구성 되어 있는 무료 앱 서비스 계획과 무료 계층으로 오지 hello SQL 데이터베이스 및 Azure Redis Cache에 대 한 필요한 저렴 한 비용 옵션을 호스팅에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![TooAzure 배포][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="e51d5-312">Hello 페이지, 읽기 hello 약관의 toohello 끝 스크롤하여 hello 확인 hello 필요한 설정을 구성한 후 **toohello 약관 위에서 설명한 동의** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="e51d5-313">hello 리소스를 프로 비전 toobegin, 클릭 **구매**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="e51d5-314">배포의 tooview hello 진행률 hello 알림 아이콘을 클릭 하 고 클릭 **배포 시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![배포가 시작됨][cache-deployment-started]

<span data-ttu-id="e51d5-316">Hello에 배포의 hello 상태를 볼 수 있습니다 **Microsoft.Template** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![TooAzure 배포][cache-deploy-to-azure-step-3]

<span data-ttu-id="e51d5-318">프로 비전 완료 되 면 Visual Studio에서 응용 프로그램 tooAzure 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="e51d5-319">Hello에 hello를 프로 비전 프로세스 중 발생할 수 있는 모든 오류가 표시 **Microsoft.Template** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="e51d5-320">일반적인 오류는 너무 많은 SQL 서버 또는 구독에 따라 계획을 호스팅하는 너무 많은 무료 앱 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="e51d5-321">모든 오류를 해결 하 고 클릭 하 여 hello 프로세스를 다시 시작 **재배포** hello에 **Microsoft.Template** 블레이드 나 hello **tooAzure 배포** 이 자습서에서는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="e51d5-322">Hello 응용 프로그램 tooAzure 게시</span><span class="sxs-lookup"><span data-stu-id="e51d5-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="e51d5-323">Hello 자습서의이 단계에서는 응용 프로그램 tooAzure hello를 게시 하 고 hello 클라우드에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="e51d5-324">마우스 오른쪽 단추로 클릭 hello **ContosoTeamStats** Visual Studio에서 프로젝트를 마우스 선택 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![게시][cache-publish-app]
2. <span data-ttu-id="e51d5-326">**Microsoft Azure App Service**를 클릭하고 **기존 항목 선택**을 선택한 다음 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![게시][cache-publish-to-app-service]
3. <span data-ttu-id="e51d5-328">Hello 리소스를 포함 하는 hello 리소스 그룹을 확장 hello Azure 리소스를 작성 하 고 선택 hello 원하는 웹 응용 프로그램을 사용 하는 hello 구독을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="e51d5-329">Hello를 사용 하는 경우 **tooAzure 배포** 웹 응용 프로그램 이름으로 시작 하는 단추 **웹 사이트** 뒤에 몇 가지 추가 문자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![웹앱 선택][cache-select-web-app]
4. <span data-ttu-id="e51d5-331">클릭 **확인** toobegin hello 게시 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="e51d5-332">몇 분 후 게시 프로세스는 hello 및 샘플 응용 프로그램을 실행 하는 hello로 브라우저 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="e51d5-333">를 게시 하거나 유효성을 검사할 때 DNS 오류 hello로 프로 비전 프로세스에 대 한 hello hello 응용 프로그램에 대 한 Azure 리소스 최근에 완료 된, 잠시 기다렸다가 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e51d5-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![캐시 추가됨][cache-added-to-application]

<span data-ttu-id="e51d5-335">hello 다음 설명 hello 샘플 응용 프로그램에서 각 작업 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="e51d5-336">동작</span><span class="sxs-lookup"><span data-stu-id="e51d5-336">Action</span></span> | <span data-ttu-id="e51d5-337">설명</span><span class="sxs-lookup"><span data-stu-id="e51d5-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e51d5-338">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="e51d5-338">Create New</span></span> |<span data-ttu-id="e51d5-339">새 팀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-339">Create a new Team.</span></span> |
| <span data-ttu-id="e51d5-340">시즌 재생</span><span class="sxs-lookup"><span data-stu-id="e51d5-340">Play Season</span></span> |<span data-ttu-id="e51d5-341">게임, 업데이트 hello 팀 통계 시즌 재생 하 고 팀 데이터 hello 캐시에서 오래 된 모든 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="e51d5-342">캐시 지우기</span><span class="sxs-lookup"><span data-stu-id="e51d5-342">Clear Cache</span></span> |<span data-ttu-id="e51d5-343">Hello 캐시에서 지우기 hello 팀 통계입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="e51d5-344">캐시에서 목록</span><span class="sxs-lookup"><span data-stu-id="e51d5-344">List from Cache</span></span> |<span data-ttu-id="e51d5-345">Hello 캐시에서 hello 팀 통계를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="e51d5-346">캐시 누락 이면 hello stats hello 데이터베이스에서 로드 하 고에 toohello 캐시를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="e51d5-347">캐시에서 정렬된 집합</span><span class="sxs-lookup"><span data-stu-id="e51d5-347">Sorted Set from Cache</span></span> |<span data-ttu-id="e51d5-348">정렬된 된 집합을 사용 하 여 hello 캐시에서 hello 팀 통계를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="e51d5-349">캐시 누락 이면 hello 데이터베이스에서 hello 통계를 로드 하 고 정렬된 된 집합을 사용 하 여 toohello 캐시를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="e51d5-350">캐시에서 상위 5개 팀</span><span class="sxs-lookup"><span data-stu-id="e51d5-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="e51d5-351">정렬된 된 집합을 사용 하 여 hello 캐시에서 hello 상위 5 개 팀을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="e51d5-352">캐시 누락 이면 hello 데이터베이스에서 hello 통계를 로드 하 고 정렬된 된 집합을 사용 하 여 toohello 캐시를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="e51d5-353">DB에서 로드</span><span class="sxs-lookup"><span data-stu-id="e51d5-353">Load from DB</span></span> |<span data-ttu-id="e51d5-354">Hello 데이터베이스에서 hello 팀 통계를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="e51d5-355">DB 다시 빌드</span><span class="sxs-lookup"><span data-stu-id="e51d5-355">Rebuild DB</span></span> |<span data-ttu-id="e51d5-356">Hello 데이터베이스를 다시 작성 하 고 샘플 팀 데이터로 다시 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="e51d5-357">편집 / 세부 정보 / 삭제</span><span class="sxs-lookup"><span data-stu-id="e51d5-357">Edit / Details / Delete</span></span> |<span data-ttu-id="e51d5-358">팀을 편집하고 팀에 대한 세부 정보를 보고 팀을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="e51d5-359">Hello 동작 중 일부를 클릭 하 고 실험 hello 서로 다른 원본의 hello 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="e51d5-360">하지: hello 시간이 toocomplete hello hello 데이터베이스와 hello 캐시에서 hello 데이터를 검색 하는 여러 가지의 hello 차이</span><span class="sxs-lookup"><span data-stu-id="e51d5-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="e51d5-361">Hello 응용 프로그램을 사용 하 여 완료 하는 경우 hello 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="e51d5-362">Hello 예제 자습서 응용 프로그램으로 완료 되 면 Azure hello 삭제할 수 있습니다 순서 tooconserve 비용에 사용 되는 리소스 및 리소스.</span><span class="sxs-lookup"><span data-stu-id="e51d5-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="e51d5-363">Hello를 사용 하는 경우 **tooAzure 배포** hello 단추 [프로 비전 hello Azure 리소스](#provision-the-azure-resources) 섹션과 모든 리소스 hello에 포함 된 동일한 리소스 그룹을 삭제할 수 있습니다 이러한 함께 하나 hello 리소스 그룹을 삭제 하 여 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="e51d5-364">Toohello 로그인 [Azure 포털](https://portal.azure.com) 클릭 **리소스 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="e51d5-365">Hello에 리소스 그룹의 유형 hello 이름을 **항목 필터링...**  텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="e51d5-366">클릭 **중...**  toohello 리소스 그룹의 오른쪽입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="e51d5-367">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-367">Click **Delete**.</span></span>
   
    ![삭제][cache-delete-resource-group]
5. <span data-ttu-id="e51d5-369">리소스 그룹을 클릭 하 여의 형식 hello 이름을 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![삭제 확인][cache-delete-confirm]

<span data-ttu-id="e51d5-371">후 몇 분 정도의 hello 리소스 그룹 및 모든 포함 된 리소스가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e51d5-372">리소스 그룹을 삭제 하면 되돌릴 수 없습니다는 하 고 있는 hello 리소스 그룹을 모든 hello 리소스가 영구적으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="e51d5-373">삭제 하지 않는 실수로 hello 잘못 된 리소스 그룹 또는 리소스 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="e51d5-374">이 예제는 기존 리소스 그룹의 내부 호스팅을 위한 hello 리소스를 만든 경우 각 해당 블레이드에서 개별적으로 각 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="e51d5-375">로컬 컴퓨터의 hello 샘플 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="e51d5-376">Azure Redis Cache 필요한 컴퓨터에 로컬로 toorun hello 응용 프로그램 데이터는 toocache 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="e51d5-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="e51d5-377">Hello 이전 섹션에 설명 된 대로 응용 프로그램 tooAzure에 게시 한 경우에 해당 단계에서 프로 비전 된 hello Azure Redis 캐시 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="e51d5-378">기존 Azure Redis Cache의 다른 인스턴스를 설정한 경우 사용할 수 있습니다 해당 toorun이이 샘플 로컬로.</span><span class="sxs-lookup"><span data-stu-id="e51d5-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="e51d5-379">hello 단계를 수행 toocreate Azure Redis Cache 인스턴스 해야 할 경우 [캐시 만들기](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="e51d5-380">선택 하거나 hello 캐시 toouse 생성 되 면 hello Azure 포털에서에서 toohello 캐시 찾아 hello 검색 [호스트 이름](cache-configure.md#properties) 및 [액세스 키](cache-configure.md#access-keys) 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="e51d5-381">지침은 [Redis Cache 설정 구성](cache-configure.md#configure-redis-cache-settings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e51d5-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="e51d5-382">열기 hello `WebAppPlusCacheAppSecrets.config` hello 중에 만들어진 파일 [hello 응용 프로그램 toouse Redis 캐시 구성](#configure-the-application-to-use-redis-cache) hello 원하는 편집기를 사용 하 여이 자습서의 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="e51d5-383">Hello 편집 `value` 특성 및 바꾸기 `MyCache.redis.cache.windows.net` hello로 [호스트 이름](cache-configure.md#properties) 캐시 hello 중 하나를 지정 하 고 [기본 또는 보조 키](cache-configure.md#access-keys) hello 암호와 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="e51d5-384">키를 눌러 **Ctrl + f 5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="e51d5-385">Hello 데이터베이스를 포함 하는 hello 응용 프로그램을 로컬로 실행 되 고 hello Redis Cache에서에서 호스팅되는 Azure hello 캐시는 toounder 나타날 수-hello 데이터베이스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="e51d5-386">최상의 성능을 위해 클라이언트 응용 프로그램을 hello 및 Azure Redis Cache 인스턴스 hello에 있어야 합니다. 동일한 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e51d5-387">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e51d5-387">Next steps</span></span>
* <span data-ttu-id="e51d5-388">에 대 한 자세한 내용은 [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) hello에 [ASP.NET](http://asp.net/) 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="e51d5-389">앱 서비스에서 ASP.NET 웹 응용 프로그램을 만드는의 더 많은 예제를 참조 하십시오. [만들기 및 Azure 앱 서비스에서 ASP.NET 웹 응용 프로그램 배포](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) hello에서 [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 연결 [데모](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="e51d5-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="e51d5-390">Hello HealthClinic.biz 데모에서 자세한 퀵 스타트를 참조 하십시오. [Azure 개발자 도구 퀵 스타트](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="e51d5-391">Hello에 대 한 자세한 [코드 첫 번째 tooa 새 데이터베이스](https://msdn.microsoft.com/data/jj193542) tooEntity이이 자습서에 사용 되는 프레임 워크에 접근 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="e51d5-392">[Azure 앱 서비스의 웹앱](../app-service-web/app-service-web-overview.md)에 더 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="e51d5-393">너무 방법에 대해 알아봅니다[모니터](cache-how-to-monitor.md) hello Azure 포털에서에서 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="e51d5-394">Azure Redis Cache 프리미엄 계층 탐색</span><span class="sxs-lookup"><span data-stu-id="e51d5-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="e51d5-395">어떻게 Premium Azure Redis Cache에 대 한 tooconfigure 지 속성</span><span class="sxs-lookup"><span data-stu-id="e51d5-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="e51d5-396">어떻게 tooconfigure Premium Azure Redis Cache에 대 한 클러스터링</span><span class="sxs-lookup"><span data-stu-id="e51d5-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="e51d5-397">프리미엄 Azure Redis Cache에 대 한 tooconfigure 가상 네트워크를 지 원하는 방법</span><span class="sxs-lookup"><span data-stu-id="e51d5-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="e51d5-398">Hello 참조 [Azure Redis 캐시 FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) 크기, 처리량 및 프리미엄 캐시와 대역폭에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51d5-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

