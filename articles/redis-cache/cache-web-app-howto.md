---
title: "Redis Cache를 사용하여 웹앱을 만드는 방법 | Microsoft 문서"
description: "Redis Cache를 사용하여 웹앱을 만드는 방법 알아보기"
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
ms.openlocfilehash: f23f71cc01eccf17d36885f786de9a7517606803
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="ef223-103">Redis Cache를 사용하여 웹앱을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="ef223-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef223-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ef223-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="ef223-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ef223-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="ef223-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ef223-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="ef223-107">Java</span><span class="sxs-lookup"><span data-stu-id="ef223-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="ef223-108">Python</span><span class="sxs-lookup"><span data-stu-id="ef223-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="ef223-109">이 자습서에서는 Visual Studio 2017을 사용하여 Azure App Service에서 ASP.NET 웹 응용 프로그램을 만들고 웹앱에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="ef223-110">샘플 응용 프로그램은 데이터베이스에서 팀 통계 목록을 표시하고 Azure Redis Cache를 사용하여 캐시에서 데이터를 저장 및 검색하는 여러 가지 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="ef223-111">이 자습서를 완료하면 Azure Redis Cache에 최적화되고 Azure에서 호스팅되며 데이터베이스에 읽고 쓰는 실행 웹앱을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="ef223-112">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-112">You'll learn:</span></span>

* <span data-ttu-id="ef223-113">Visual Studio에서 ASP.NET MVC 5 웹 응용 프로그램을 만드는 방법.</span><span class="sxs-lookup"><span data-stu-id="ef223-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="ef223-114">Entity Framework를 사용하여 데이터베이스에서 데이터에 액세스하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ef223-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="ef223-115">Azure Redis Cache를 사용하여 데이터를 저장 및 검색하여 데이터 처리 능력을 개선하고 데이터베이스 부하를 줄이는 방법.</span><span class="sxs-lookup"><span data-stu-id="ef223-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="ef223-116">Redis 정렬된 집합을 사용하여 상위 5개 팀을 검색하도록 설정하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ef223-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="ef223-117">Resource Manager 템플릿을 사용하여 응용 프로그램에 대한 Azure 리소스를 프로비전하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ef223-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="ef223-118">Visual Studio를 사용하여 응용 프로그램을 Azure에 게시하는 방법.</span><span class="sxs-lookup"><span data-stu-id="ef223-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef223-119">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ef223-119">Prerequisites</span></span>
<span data-ttu-id="ef223-120">자습서를 완료하려면 다음 필수 구성 요소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="ef223-121">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="ef223-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="ef223-122">.NET용 Azure SDK 포함 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ef223-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="ef223-123">Azure 계정</span><span class="sxs-lookup"><span data-stu-id="ef223-123">Azure account</span></span>
<span data-ttu-id="ef223-124">이 자습서를 완료하려면 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="ef223-125">다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-125">You can:</span></span>

* <span data-ttu-id="ef223-126">[Azure 계정을 무료로 개설할 수 있습니다](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="ef223-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="ef223-127">유료 Azure 서비스를 사용해볼 수 있는 크레딧을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="ef223-128">크레딧을 모두 사용한 후에도 계정을 유지하고 무료 Azure 서비스 및 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="ef223-129">[Visual Studio 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero)</span><span class="sxs-lookup"><span data-stu-id="ef223-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="ef223-130">MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="ef223-131">.NET용 Azure SDK 포함 Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ef223-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="ef223-132">자습서는 [Azure SDK for.NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools)이 포함된 Visual Studio 2017을 기준으로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="ef223-133">Azure SDK 2.9.5에는 Visual Studio 설치 관리자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="ef223-134">Visual Studio 2015가 설치된 경우 [Azure SDK for.NET](../dotnet-sdk.md) 2.8.2 이상을 포함한 자습서를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="ef223-135">[여기서 Visual Studio 2015용 최신 Azure SDK를 다운로드](http://go.microsoft.com/fwlink/?linkid=518003)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="ef223-136">SDK가 없는 경우 Visual Studio는 SDK와 함께 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="ef223-137">일부 화면이 이 자습서에 표시된 그림과 다르게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="ef223-138">Visual Studio 2013이 있는 경우 [최신 Visual Studio 2013용 Azure SDK를 다운로드](http://go.microsoft.com/fwlink/?LinkID=324322)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="ef223-139">일부 화면이 이 자습서에 표시된 그림과 다르게 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="ef223-140">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="ef223-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="ef223-141">Visual Studio를 열고 **파일**, **새로 만들기**, **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="ef223-142">**템플릿** 목록에서 **Visual C#** 노드를 확장하고 **클라우드**를 선택한 다음 **ASP.NET 웹 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="ef223-143">**.NET Framework 4.5.2** 이상이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="ef223-144">**이름** 텍스트 상자에 **ContosoTeamStats**를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![프로젝트 만들기][cache-create-project]
3. <span data-ttu-id="ef223-146">프로젝트 유형으로 **MVC** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="ef223-147">**인증** 설정에 **인증 없음**을 지정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="ef223-148">Visual Studio의 버전에 따라 다른 기본값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="ef223-149">변경하려면 **인증 변경**을 클릭하고 **인증 없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="ef223-150">Visual Studio 2015에서 수행하는 경우 **클라우드에서 호스트** 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="ef223-151">자습서의 이후 단계에서는 [Azure 리소스를 프로비전](#provision-the-azure-resources)하고 [응용 프로그램을 Azure에 게시](#publish-the-application-to-azure)합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="ef223-152">**클라우드에서 호스트** 를 선택된 채로 두고 Visual Studio에서 앱 서비스 웹앱을 프로비전하는 예제는 [ASP.NET 및 Visual Studio를 사용하여 Azure 앱 서비스에서 웹앱 시작하기](../app-service-web/app-service-web-get-started-dotnet.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![프로젝트 템플릿 선택][cache-select-template]
4. <span data-ttu-id="ef223-154">**확인** 을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="ef223-155">ASP.NET MVC 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="ef223-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="ef223-156">자습서의 이 섹션에서는 데이터베이스에서 팀 통계를 읽고 표시하는 기본 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="ef223-157">Entity Framework NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="ef223-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="ef223-158">모델 추가</span><span class="sxs-lookup"><span data-stu-id="ef223-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="ef223-159">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="ef223-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="ef223-160">보기 구성</span><span class="sxs-lookup"><span data-stu-id="ef223-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="ef223-161">Entity Framework NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="ef223-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="ef223-162">**도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="ef223-163">**패키지 관리자 콘솔** 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="ef223-164">이 패키지에 대한 자세한 내용은 [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="ef223-165">모델 추가</span><span class="sxs-lookup"><span data-stu-id="ef223-165">Add the model</span></span>
1. <span data-ttu-id="ef223-166">**솔루션 탐색기**에서 **모델**을 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![모델 추가][cache-model-add-class]
2. <span data-ttu-id="ef223-168">클래스 이름으로 `Team` 을 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![모델 클래스 추가][cache-model-add-class-dialog]
3. <span data-ttu-id="ef223-170">`Team.cs` 파일의 위쪽에 있는 `using` 문을 다음 `using` 문으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="ef223-171">`Team` 클래스의 정의를 업데이트된 `Team` 클래스 정의뿐만 아니라 몇몇 다른 Entity Framework 도우미 클래스도 포함하고 있는 다음 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="ef223-172">이 자습서에 사용되는 Entity Framework에 대한 Code First 접근방식에 대한 자세한 내용은 [새 데이터베이스에 대한 Code First](https://msdn.microsoft.com/data/jj193542)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="ef223-173">**솔루션 탐색기**에서 **web.config**를 두 번 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="ef223-175">다음 `connectionStrings` 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="ef223-176">연결 문자열의 이름은 `TeamContext`인 Entity Framework 데이터베이스 컨텍스트 클래스의 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="ef223-177">새 `connectionStrings` 섹션을 추가하여 다음 예제와 같이 `configSections` 뒤에 오도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

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
    > <span data-ttu-id="ef223-178">연결 문자열은 자습서를 작성하는 데 사용된 Visual Studio 및 SQL Server Express 버전에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-178">Your connection string may be different depending on the version of Visual Studio and SQL Server Express edition used to complete the tutorial.</span></span> <span data-ttu-id="ef223-179">설치에 맞게 Web.config 템플릿을 구성해야 하며 `(LocalDB)\v11.0`(SQL Server Express 2012에서) 또는 `Data Source=(LocalDB)\MSSQLLocalDB`(SQL Server Express 2014 이상에서)와 같은 `Data Source` 항목이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-179">The web.config template should be configured to match your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="ef223-180">연결 문자열 및 SQL Express 버전에 대한 자세한 내용은 [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-the-controller"></a><span data-ttu-id="ef223-181">컨트롤러 추가</span><span class="sxs-lookup"><span data-stu-id="ef223-181">Add the controller</span></span>
1. <span data-ttu-id="ef223-182">**F6** 을 눌러 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-182">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="ef223-183">**솔루션 탐색기**에서 **컨트롤러** 폴더를 마우스 오른쪽 단추로 클릭하고 **추가**, **컨트롤러**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-183">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![컨트롤러 추가][cache-add-controller]
3. <span data-ttu-id="ef223-185">**Entity Framework를 사용하여 보기가 포함된 MVC 5 컨트롤러**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="ef223-186">**추가**를 클릭한 후 오류가 발생하면 먼저 프로젝트를 빌드했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-186">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![컨트롤러 클래스 추가][cache-add-controller-class]
4. <span data-ttu-id="ef223-188">**모델 클래스** 드롭다운 목록에서 **팀(ContosoTeamStats.Models)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-188">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="ef223-189">**데이터 컨텍스트 클래스** 드롭다운 목록에서 **TeamContext(ContosoTeamStats.Models)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-189">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="ef223-190">**컨트롤러** 이름 텍스트 상자에 `TeamsController`를 입력합니다(자동으로 채워지지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="ef223-190">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="ef223-191">**추가** 를 클릭하여 컨트롤러 클래스를 만들고 기본 보기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-191">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![컨트롤러 구성][cache-configure-controller]
5. <span data-ttu-id="ef223-193">**솔루션 탐색기**에서 **Global.asax**를 확장하고 **Global.asax.cs**를 두 번 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="ef223-195">파일의 위쪽에 있는 다음 두 `using` 문을 다른 `using` 문 아래에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-195">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="ef223-196">다음 코드 줄을 `Application_Start` 메서드의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-196">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="ef223-197">**솔루션 탐색기**에서 `App_Start`를 확장하고 `RouteConfig.cs`를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="ef223-199">다음 예제와 같이 `RegisterRoutes` 메서드의 다음 코드에 있는 `controller = "Home"`을 `controller = "Teams"`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-199">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="ef223-200">보기 구성</span><span class="sxs-lookup"><span data-stu-id="ef223-200">Configure the views</span></span>
1. <span data-ttu-id="ef223-201">**솔루션 탐색기**에서 **보기** 폴더, **공유** 폴더를 차례로 확장하고 **_Layout.cshtml**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-201">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="ef223-203">다음 예제와 같이 `title` 요소의 내용을 변경하고 `My ASP.NET Application`을 `Contoso Team Stats`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-203">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="ef223-204">`body` 섹션에서 첫 번째 `Html.ActionLink` 문을 업데이트하고 `Application name`을 `Contoso Team Stats`로 바꾸고 `Home`을 `Teams`로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-204">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="ef223-205">이전: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="ef223-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="ef223-206">이후: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="ef223-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![코드 변경 내용][cache-layout-cshtml-code]
2. <span data-ttu-id="ef223-208">**Ctrl+F5** 키를 눌러 응용 프로그램을 빌드 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-208">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="ef223-209">이 버전의 응용 프로그램이 데이터베이스에서 직접 결과를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-209">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="ef223-210">참고로 **새로 만들기**, **편집**, **세부 정보** 및 **삭제** 작업은 응용 프로그램에 **Entity Framework를 사용하는 보기 포함 MVC 5 컨트롤러** 스캐폴드에 의해 자동으로 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-210">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="ef223-211">자습서의 다음 섹션에서는 데이터 액세스를 최적화하고 응용 프로그램에 추가 기능을 제공하기 위해 Redis Cache를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-211">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![시작 응용 프로그램][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="ef223-213">Redis Cache를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ef223-213">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="ef223-214">자습서의 이 섹션에서는 [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) 캐시 클라이언트를 사용하여 Azure Redis Cache 인스턴스에서 Contoso 팀 통계를 저장 및 검색하도록 샘플 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-214">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="ef223-215">StackExchange.Redis를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ef223-215">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="ef223-216">캐시 또는 데이터베이스에서 결과를 반환하도록 TeamsController 클래스 업데이트</span><span class="sxs-lookup"><span data-stu-id="ef223-216">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="ef223-217">캐시로 작업하도록 Create, Edit 및 Delete 메서드 업데이트</span><span class="sxs-lookup"><span data-stu-id="ef223-217">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="ef223-218">캐시로 작업하도록 팀 인덱스 보기 업데이트</span><span class="sxs-lookup"><span data-stu-id="ef223-218">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="ef223-219">StackExchange.Redis를 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="ef223-219">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="ef223-220">StackExchange.Redis NuGet 패키지를 사용하여 Visual Studio에서 클라이언트 응용 프로그램을 구성하려면 **도구** 메뉴에서 **NuGet 패키지 관리자**, **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-220">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="ef223-221">`Package Manager Console` 창에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-221">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="ef223-222">NuGet 패키지는 클라이언트 응용 프로그램이 StackExchange.Redis 캐시 클라이언트를 사용하여 Azure Redis 캐시에 액세스하는 는 데 필요한 어셈블리 참조를 다운로드하고 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-222">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="ef223-223">강력한 이름의 `StackExchange.Redis` 클라이언트 라이브러리 버전을 사용하려는 경우 `StackExchange.Redis.StrongName` 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-223">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="ef223-224">**솔루션 탐색기**에서 **컨트롤러** 폴더를 확장하고 **TeamsController.cs**를 두 번 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-224">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![팀 컨트롤러][cache-teamscontroller]
4. <span data-ttu-id="ef223-226">**TeamsController.cs**에 다음 두 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-226">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="ef223-227">`TeamsController` 클래스에 다음 두 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-227">Add the following two properties to the `TeamsController` class.</span></span>

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

6. <span data-ttu-id="ef223-228">컴퓨터에 `WebAppPlusCacheAppSecrets.config` 라는 파일을 만들고 이 파일을 다른 위치에서 체크인하기로 결정한 경우 샘플 응용 프로그램의 소스 코드에서 체크인하지 않을 위치에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="ef223-229">이 예제에서 `AppSettingsSecrets.config` 파일은 `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-229">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="ef223-230">`WebAppPlusCacheAppSecrets.config` 파일을 편집하여 다음 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-230">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="ef223-231">응용 프로그램을 로컬로 실행하는 경우 이 정보는 Azure Redis Cache 인스턴스를 연결하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-231">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="ef223-232">이 자습서의 뒷부분에서는 Azure Redis Cache 인스턴스를 프로비전하고 캐시 이름 및 암호를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-232">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="ef223-233">샘플 응용 프로그램을 로컬로 실행할 계획이 아닌 경우, Azure에 배포할 때 응용 프로그램이 이 파일이 아닌 웹앱에 대한 앱 설정에서 캐시 연결 정보를 검색하므로 이 파일 만들기 및 해당 파일을 참조하는 이후 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-233">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="ef223-234">`WebAppPlusCacheAppSecrets.config` 는 응용 프로그램과 함께Azure에 배포되지 않으므로 응용 프로그램을 로컬로 실행하려는 경우가 아니면 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-234">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="ef223-235">**솔루션 탐색기**에서 **web.config**를 두 번 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-235">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="ef223-237">다음 `file` 속성을 `appSettings` 요소에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-237">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="ef223-238">다른 파일 이름 또는 위치를 사용한 경우, 예제에 나타난 값을 해당 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-238">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="ef223-239">이전: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="ef223-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="ef223-240">이후: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="ef223-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="ef223-241">ASP.NET 런타임은 외부 파일의 내용을 `<appSettings>` 요소의 태그와 병합합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-241">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="ef223-242">지정된 파일을 찾을 수 없는 경우 런타임에서 파일 특성을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-242">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="ef223-243">암호(캐시에 대한 연결 문자열)는 응용 프로그램에 대 한 소스 코드의 일부분으로 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-243">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="ef223-244">Azure에 웹앱을 배포하는 경우 `WebAppPlusCacheAppSecrests.config` 파일은 배포되지 않습니다(즉, 원하는 상태임).</span><span class="sxs-lookup"><span data-stu-id="ef223-244">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="ef223-245">Azure에서 이러한 암호를 지정하는 여러 가지 방법이 있으며 이 자습서에서는 이후 단계에서 [Azure 리소스를 프로비전](#provision-the-azure-resources) 할 때 암호가 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-245">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="ef223-246">Azure에서 암호로 작업에 대한 자세한 내용은 [ASP.NET 및 Azure 앱 서비스에 암호 및 기타 중요한 데이터 배포를 위한 모범 사례](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="ef223-247">캐시 또는 데이터베이스에서 결과를 반환하도록 TeamsController 클래스 업데이트</span><span class="sxs-lookup"><span data-stu-id="ef223-247">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="ef223-248">이 샘플에서는 데이터베이스 또는 캐시에서 팀 통계를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-248">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="ef223-249">팀 통계는 직렬화된 `List<Team>`으로 캐시에 저장되며 Redis 데이터 유형을 사용하여 정렬된 집합으로도 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-249">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="ef223-250">정렬된 집합에서 항목을 검색하는 경우 일부 또는 모두 검색하거나 특정 항목을 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="ef223-251">이 샘플에서는 정렬된 집합에서 승리 횟수 순으로 상위 5개 팀을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-251">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="ef223-252">Azure Redis Cache를 사용하려는 경우 여러 형식의 팀 통계를 캐시에 저장할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-252">It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache.</span></span> <span data-ttu-id="ef223-253">이 자습서에서는 여러 형식을 사용하여 데이터를 캐시하는 데 사용할 수 있는 몇 가지 방법 및 여러 가지 데이터 형식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-253">This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.</span></span>
> 
> 

1. <span data-ttu-id="ef223-254">다음 `using` 문을 다른 `using` 문과 함께 위쪽의 `TeamsController.cs` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-254">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="ef223-255">현재 `public ActionResult Index()` 메서드 구현을 다음 구현으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-255">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

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

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="ef223-256">이전 코드 조각에 추가된 switch 문에서 `playGames`, `clearCache` 및 `rebuildDB` 작업을 구현하기 위해 다음 세 가지 메서드를 `TeamsController` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-256">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="ef223-257">`PlayGames` 메서드는 게임 시즌을 시뮬레이션하여 팀 통계를 업데이트하고 결과를 데이터베이스에 저장하고 이제 만료된 데이터를 캐시에서 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-257">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

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

    <span data-ttu-id="ef223-258">`RebuildDB` 메서드는 데이터베이스를 기본 팀 집합으로 다시 초기화하고 그에 대한 통계를 생성하고 이제 만료된 데이터를 캐시에서 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-258">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="ef223-259">`ClearCachedTeams` 메서드는 캐시된 모든 팀 통계를 캐시에서 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-259">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="ef223-260">캐시 및 데이터베이스에서 팀 통계를 검색하는 여러 가지 방법을 구현하기 위해 다음 네 가지 메서드를 `TeamsController` 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-260">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="ef223-261">이러한 각 메서드는 `List<Team>` 를 반환하며 이는 보기에 의해 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-261">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="ef223-262">`GetFromDB` 메서드는 팀 통계를 데이터베이스에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-262">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
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

    <span data-ttu-id="ef223-263">`GetFromList` 메서드는 팀 통계를 직렬화된 `List<Team>`으로 캐시에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-263">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="ef223-264">캐시 누락이 있는 경우 팀 통계를 데이터베이스에서 읽은 후 다음에 캐시에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-264">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="ef223-265">이 샘플에서는 JSON.NET 직렬화를 사용하여 .NET 개체를 캐시에 대해 직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-265">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="ef223-266">자세한 내용은 [Azure Redis Cache에서 .NET 개체로 작업하는 방법](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-266">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="ef223-267">`GetFromSortedSet` 메서드는 캐시된 정렬된 집합에서 팀 통계를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-267">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="ef223-268">캐시 누락이 있는 경우 팀 통계를 데이터베이스에서 읽은 후 정렬된 집합으로 캐시에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-268">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
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

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="ef223-269">`GetFromSortedSetTop5` 메서드는 캐시된 정렬된 집합에서 상위 5개 팀을 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-269">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="ef223-270">먼저 캐시에서 `teamsSortedSet` 키의 유무를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-270">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="ef223-271">이 키가 없는 경우 `GetFromSortedSet` 메서드를 호출하여 팀 통계를 읽고 캐시에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-271">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="ef223-272">그런 다음 캐시된 정렬된 집합에 대해 반환된 상위 5개 팀을 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-272">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="ef223-273">캐시로 작업하도록 Create, Edit 및 Delete 메서드 업데이트</span><span class="sxs-lookup"><span data-stu-id="ef223-273">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="ef223-274">이 샘플의 일부로 생성된 스캐폴딩 코드는 팀을 추가, 편집 및 삭제하는 메서드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-274">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="ef223-275">팀이 추가, 편집 또는 제거될 때마다 캐시의 데이터가 만료됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-275">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="ef223-276">이 섹션에서는 캐시와 데이터베이스의 동기화가 해제되지 않도록 캐시된 팀을 지우도록 이러한 세 가지 메서드를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-276">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="ef223-277">`TeamsController` 클래스의 `Create(Team team)` 메서드를 찾아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-277">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="ef223-278">다음 예제와 같이 `ClearCachedTeams` 메서드 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-278">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="ef223-279">`TeamsController` 클래스의 `Edit(Team team)` 메서드를 찾아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-279">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="ef223-280">다음 예제와 같이 `ClearCachedTeams` 메서드 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-280">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="ef223-281">`TeamsController` 클래스의 `DeleteConfirmed(int id)` 메서드를 찾아갑니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-281">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="ef223-282">다음 예제와 같이 `ClearCachedTeams` 메서드 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-282">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="ef223-283">캐시로 작업하도록 팀 인덱스 보기 업데이트</span><span class="sxs-lookup"><span data-stu-id="ef223-283">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="ef223-284">**솔루션 탐색기**에서 **보기** 폴더, **팀** 폴더를 차례로 확장한 다음 **Index.cshtml**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-284">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="ef223-286">파일의 위쪽 부근에서 다음 단락 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-286">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![작업 테이블][cache-teams-index-table]
   
    <span data-ttu-id="ef223-288">새 팀을 만들 수 있는 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-288">This is the link to create a new team.</span></span> <span data-ttu-id="ef223-289">단락 요소를 다음 테이블로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-289">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="ef223-290">이 테이블에는 새 게임 시즌 실행, 캐시 지우기, 여러 형식의 캐시에서 팀 검색, 데이터베이스에서 팀 검색 및 새 샘플 데이터를 사용하여 데이터베이스 다시 빌드를 수행할 수 있는 작업 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-290">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

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


1. <span data-ttu-id="ef223-291">**Index.cshtml** 파일의 아래쪽으로 스크롤하고 다음 `tr` 요소를 파일의 마지막 테이블에서 마지막 행이 되도록 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-291">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="ef223-292">이 행은 현재 작업에 대한 상태 보고서를 포함하는 `ViewBag.Msg` 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-292">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="ef223-293">`ViewBag.Msg`은 이전 단계에서 작업 링크를 클릭할 때 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-293">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![상태 메시지][cache-status-message]
2. <span data-ttu-id="ef223-295">**F6** 을 눌러 프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-295">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="ef223-296">Azure 리소스를 프로비전</span><span class="sxs-lookup"><span data-stu-id="ef223-296">Provision the Azure resources</span></span>
<span data-ttu-id="ef223-297">응용 프로그램을 Azure에서 호스트하려면 먼저 응용 프로그램에 필요한 Azure 서비스를 프로비전해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-297">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="ef223-298">이 자습서의 샘플 응용 프로그램에서는 다음 Azure 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-298">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="ef223-299">Azure Redis 캐시(영문)</span><span class="sxs-lookup"><span data-stu-id="ef223-299">Azure Redis Cache</span></span>
* <span data-ttu-id="ef223-300">앱 서비스 웹앱</span><span class="sxs-lookup"><span data-stu-id="ef223-300">App Service Web App</span></span>
* <span data-ttu-id="ef223-301">SQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="ef223-301">SQL Database</span></span>

<span data-ttu-id="ef223-302">선택한 새 또는 기존 리소스 그룹에 이러한 서비스를 배포하려면 다음 **Azure에 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-302">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="ef223-303">[![Azure에 배포][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ef223-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="ef223-304">이 **Azure에 배포** 단추는 [Web App 및 Redis Cache 및 SQL Database 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure 빠른 시작](https://github.com/Azure/azure-quickstart-templates) 템플릿을 사용하여 이러한 서비스를 프로비전하고 SQL Database에 대한 연결 문자열을 설정하고 Azure Redis Cache 연결 문자열에 대한 응용 프로그램 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-304">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="ef223-305">Azure 계정이 없는 경우 몇 분 만에 [무료 계정을 만들](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="ef223-306">**Azure에 배포** 단추를 클릭하면 Azure 포털로 이동하며 템플릿에서 설명한 리소스 만들기 과정을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-306">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![Deploy to Azure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="ef223-308">**기본 사항** 섹션에서 사용할 Azure 구독을 선택하고 기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만들고 리소스 그룹 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-308">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="ef223-309">**설정** 섹션에서 **관리자 로그인**(**admin** 사용 안 함), **관리자 로그인 암호** 및 **데이터베이스 이름**을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-309">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="ef223-310">다른 매개 변수는 무료 앱 서비스 호스팅 계획을 위해 구성되며 더 낮은 비용 옵션은 SQL Database 및 무료 계층으로 제공되지 않는 Azure Redis Cache를 위해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-310">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Deploy to Azure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="ef223-312">원하는 설정을 구성한 후 페이지 끝으로 스크롤하여 사용 약관을 읽고 **위에 명시된 사용 약관에 동의함** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-312">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="ef223-313">리소스 프로비전을 시작하려면 **구매**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-313">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="ef223-314">배포의 진행률을 보려면 알림 아이콘을 클릭하고 **배포가 시작됨**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-314">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![배포가 시작됨][cache-deployment-started]

<span data-ttu-id="ef223-316">**Microsoft.Template** 블레이드에서 배포의 상태를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-316">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![Azure에 배포][cache-deploy-to-azure-step-3]

<span data-ttu-id="ef223-318">프로비전이 완료되면 Visual Studio에서 Azure에 응용 프로그램을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-318">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="ef223-319">프로비전 프로세스 중에 발생할 수 있는 오류는 **Microsoft.Template** 블레이드에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-319">Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade.</span></span> <span data-ttu-id="ef223-320">일반적인 오류는 너무 많은 SQL 서버 또는 구독에 따라 계획을 호스팅하는 너무 많은 무료 앱 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="ef223-321">**Microsoft.Template** 블레이드의 **재배포** 또는 이 자습서의 **Azure에 배포** 단추를 클릭하여 오류를 해결하고 프로세스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-321">Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="ef223-322">응용 프로그램을 Azure에 게시</span><span class="sxs-lookup"><span data-stu-id="ef223-322">Publish the application to Azure</span></span>
<span data-ttu-id="ef223-323">자습서의 이 단계에서는 Azure에 응용 프로그램을 게시하고 클라우드에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-323">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="ef223-324">Visual Studio에서 **ContosoTeamStats** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-324">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![게시][cache-publish-app]
2. <span data-ttu-id="ef223-326">**Microsoft Azure App Service**를 클릭하고 **기존 항목 선택**을 선택한 다음 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![게시][cache-publish-to-app-service]
3. <span data-ttu-id="ef223-328">Azure 리소스를 만들 때 사용한 구독을 선택하고 리소스가 포함된 리소스 그룹을 확장하고 원하는 Web App을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-328">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="ef223-329">**Azure에 배포** 단추를 사용한 경우 Web App 이름은 **webSite**로 시작하고 그 다음에 일부 추가 문자를 덧붙입니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-329">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![웹앱 선택][cache-select-web-app]
4. <span data-ttu-id="ef223-331">**확인**을 클릭하여 게시 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-331">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="ef223-332">잠시 후 게시 프로세스가 완료되며 실행 중인 샘플 응용 프로그램과 함께 브라우저가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-332">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="ef223-333">유효성 검사 또는 게시를 수행할 때 DNS 오류가 발생하고 응용 프로그램에 대한 Azure 리소스의 프로비저 프로세스가 최근에 완료된 경우 잠시 기다렸다가 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-333">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![캐시 추가됨][cache-added-to-application]

<span data-ttu-id="ef223-335">다음 테이블은 샘플 응용 프로그램에서 각 작업 링크를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-335">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="ef223-336">작업</span><span class="sxs-lookup"><span data-stu-id="ef223-336">Action</span></span> | <span data-ttu-id="ef223-337">설명</span><span class="sxs-lookup"><span data-stu-id="ef223-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef223-338">새로 만들기</span><span class="sxs-lookup"><span data-stu-id="ef223-338">Create New</span></span> |<span data-ttu-id="ef223-339">새 팀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-339">Create a new Team.</span></span> |
| <span data-ttu-id="ef223-340">시즌 재생</span><span class="sxs-lookup"><span data-stu-id="ef223-340">Play Season</span></span> |<span data-ttu-id="ef223-341">게임 시즌을 재생하고 팀 통계를 업데이트하고 만료된 팀 데이터를 캐시에서 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-341">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="ef223-342">캐시 지우기</span><span class="sxs-lookup"><span data-stu-id="ef223-342">Clear Cache</span></span> |<span data-ttu-id="ef223-343">캐시에서 팀 통계를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-343">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="ef223-344">캐시에서 목록</span><span class="sxs-lookup"><span data-stu-id="ef223-344">List from Cache</span></span> |<span data-ttu-id="ef223-345">캐시에서 팀 통계를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-345">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="ef223-346">캐시 누락이 있는 경우 데이터베이스에서 통계를 로드하고 다음에 캐시에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-346">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="ef223-347">캐시에서 정렬된 집합</span><span class="sxs-lookup"><span data-stu-id="ef223-347">Sorted Set from Cache</span></span> |<span data-ttu-id="ef223-348">정렬된 집합을 사용하여 캐시에서 팀 통계를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-348">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="ef223-349">캐시 누락이 있는 경우 데이터베이스에서 통계를 로드하고 정렬된 집합을 사용하여 캐시에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="ef223-350">캐시에서 상위 5개 팀</span><span class="sxs-lookup"><span data-stu-id="ef223-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="ef223-351">정렬된 집합을 사용하여 캐시에서 상위 5개 팀을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-351">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="ef223-352">캐시 누락이 있는 경우 데이터베이스에서 통계를 로드하고 정렬된 집합을 사용하여 캐시에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-352">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="ef223-353">DB에서 로드</span><span class="sxs-lookup"><span data-stu-id="ef223-353">Load from DB</span></span> |<span data-ttu-id="ef223-354">데이터베이스에서 팀 통계를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-354">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="ef223-355">DB 다시 빌드</span><span class="sxs-lookup"><span data-stu-id="ef223-355">Rebuild DB</span></span> |<span data-ttu-id="ef223-356">데이터베이스를 다시 빌드하고 샘플 팀 데이터와 함께 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-356">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="ef223-357">편집 / 세부 정보 / 삭제</span><span class="sxs-lookup"><span data-stu-id="ef223-357">Edit / Details / Delete</span></span> |<span data-ttu-id="ef223-358">팀을 편집하고 팀에 대한 세부 정보를 보고 팀을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="ef223-359">일부 작업을 클릭하고 다른 출처의 데이터 검색을 실험합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-359">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="ef223-360">데이터베이스 및 캐시에서 데이터를 검색하는 여러 방법을 완료하는 데 걸리는 시간 차이는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-360">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="ef223-361">응용 프로그램을 마쳤으면 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-361">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="ef223-362">샘플 자습서 응용 프로그램을 마쳤을 때 비용 및 리소스를 절감하기 위해 사용한 Azure 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-362">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="ef223-363">**Azure 리소스** 섹션의 [Azure에 배포](#provision-the-azure-resources) 단추를 사용했고 모든 리소스를 같은 리소스 그룹에 포함시킨 경우 리소스 그룹을 삭제하여 한 번의 작업으로 이들을 모두 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-363">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="ef223-364">[Azure 포털](https://portal.azure.com) 에 로그인하고 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-364">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="ef223-365">**항목 필터링...** 텍스트 상자에 리소스 그룹의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-365">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="ef223-366">리소스 그룹 오른쪽의 **...** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-366">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="ef223-367">**삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-367">Click **Delete**.</span></span>
   
    ![삭제][cache-delete-resource-group]
5. <span data-ttu-id="ef223-369">리소스 그룹의 이름을 입력하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-369">Type the name of your resource group and click **Delete**.</span></span>
   
    ![삭제 확인][cache-delete-confirm]

<span data-ttu-id="ef223-371">잠시 후 리소스 그룹 및 해당 그룹에 포함된 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-371">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef223-372">참고로 리소스 그룹 삭제는 취소할 수 없으며 해당 리소스 그룹 및 해당 그룹 안에 있는 모든 리소스는 영구적으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-372">Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="ef223-373">잘못된 리소스 그룹 또는 리소스를 자동으로 삭제하지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-373">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="ef223-374">기존 리소스 그룹 내에 있는 이 샘플을 호스트하기 위한 리소스를 만든 경우 해당 블레이드에서 각 리소스를 개별적으로 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-374">If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="ef223-375">로컬 컴퓨터에서 샘플 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-375">Run the sample application on your local machine</span></span>
<span data-ttu-id="ef223-376">응용 프로그램을 로컬로 실행하려면 데이터를 캐시하는 Azure Redis Cache 인스턴스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-376">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="ef223-377">이전 섹션에서 설명한 대로 응용 프로그램을 Azure에 게시한 경우 해당 단계에서 프로비전된 Azure Redis Cache 인스턴스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-377">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="ef223-378">다른 기존 Azure Redis Cache 인스턴스가 있는 경우 해당 인스턴스를 사용하여 이 샘플을 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-378">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="ef223-379">Azure Redis Cache 인스턴스를 만들어야 할 경우 [캐시 만들기](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache)의 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-379">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="ef223-380">사용할 캐시를 선택하거나 만든 후 Azure Portal에서 캐시를 찾아가고 캐시에 대해 [호스트 이름](cache-configure.md#properties) 및 [선택키](cache-configure.md#access-keys)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-380">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="ef223-381">지침은 [Redis Cache 설정 구성](cache-configure.md#configure-redis-cache-settings)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="ef223-382">선택한 편집기를 사용하여 [Redis Cache를 사용하도록 응용 프로그램 구성](#configure-the-application-to-use-redis-cache) 단계 중에 만든 `WebAppPlusCacheAppSecrets.config` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-382">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="ef223-383">`value` 특성을 편집하고 `MyCache.redis.cache.windows.net`을 캐시의 [호스트 이름](cache-configure.md#properties)으로 바꾸고 캐시의 [기본 또는 보조 키](cache-configure.md#access-keys)를 암호로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-383">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="ef223-384">**Ctrl+F5** 를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-384">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> <span data-ttu-id="ef223-385">데이터베이스를 비롯한 응용 프로그램이 로컬로 실행되고 Redis Cache가 Azure에서 호스트되기 때문에 캐시는 데이터베이스의 성능을 저하시키는 것처럼 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-385">Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database.</span></span> <span data-ttu-id="ef223-386">최상의 성능을 위해 클라이언트 응용 프로그램 및 Azure Redis Cache 인스턴스가 동일한 위치에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-386">For best performance, the client application and Azure Redis Cache instance should be in the same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ef223-387">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ef223-387">Next steps</span></span>
* <span data-ttu-id="ef223-388">[ASP.NET](http://asp.net/) 사이트에서 [ASP.NET MVC 5로 시작](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started)에 대해 더 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="ef223-389">앱 서비스에서 ASP.NET 웹앱을 만드는 방법의 더 많은 예제는 [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [데모](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/)에서 [Azure App Service에서 ASP.NET 웹앱 만들기 및 배포](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="ef223-390">HealthClinic.biz 데모에서 더 빠른 시작은 [Azure 개발자 도구 빠른 시작](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-390">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="ef223-391">이 자습서에 사용되는 Entity Framework에 대한 [새 데이터베이스에 Code First](https://msdn.microsoft.com/data/jj193542) 접근방식에 대해 더 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-391">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="ef223-392">[Azure 앱 서비스의 웹앱](../app-service-web/app-service-web-overview.md)에 더 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="ef223-393">Azure 포털에서 캐시를 [모니터링](cache-how-to-monitor.md) 하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ef223-393">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="ef223-394">Azure Redis Cache 프리미엄 계층 탐색</span><span class="sxs-lookup"><span data-stu-id="ef223-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="ef223-395">프리미엄 Azure Redis Cache에 지속성을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="ef223-395">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="ef223-396">프리미엄 Azure Redis Cache에 클러스터링을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="ef223-396">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="ef223-397">프리미엄 Azure Redis Cache에 가상 네트워크 지원을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="ef223-397">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="ef223-398">프리미엄 캐시에서의 크기, 처리량 및 대역폭에 대한 자세한 내용은 [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef223-398">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

