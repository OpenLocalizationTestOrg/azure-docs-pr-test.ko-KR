---
title: "Azure 클라우드 서비스 및 ASP.NET 시작: aaaGet | Microsoft Docs"
description: "자세한 내용은 방법 toocreate ASP.NET MVC 및 Azure를 사용 하 여 다중 계층 응용 프로그램입니다. hello 앱 웹 역할과 작업자 역할에는 클라우드 서비스에서 실행 됩니다. Entity Framework, SQL 데이터베이스 및 Azure 저장소 큐와 Blob를 사용합니다."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="e5593-105">Azure 클라우드 서비스 및 ASP.NET 시작</span><span class="sxs-lookup"><span data-stu-id="e5593-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="e5593-106">개요</span><span class="sxs-lookup"><span data-stu-id="e5593-106">Overview</span></span>
<span data-ttu-id="e5593-107">이 자습서에서는 어떻게 toocreate 프런트 엔드, ASP.NET mvc는 다층 계층.NET 응용 프로그램 및 tooan 배포 [Azure 클라우드 서비스](cloud-services-choose-me.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="e5593-108">응용 프로그램에서는 hello [Azure SQL 데이터베이스](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob 서비스](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), 및 hello [Azure 큐 서비스](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="e5593-109">있습니다 수 [hello Visual Studio 프로젝트를 다운로드](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) hello MSDN 코드 갤러리에서에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="e5593-110">표시 하는 hello 자습서 toobuild 및 실행 hello 응용 프로그램을 로컬로 어떻게 toodeploy 것 tooAzure 및 연속된 hello 클라우드 방법과 toobuild 처음부터 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="e5593-111">처음부터 작성 하 여 시작 하 고 닫을 수 테스트 hello 있고 원하는 경우 단계를 나중에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="e5593-112">Contoso Ads 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="e5593-112">Contoso Ads application</span></span>
<span data-ttu-id="e5593-113">hello 응용 프로그램에는 광고 게시판입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="e5593-114">사용자는 텍스트를 입력하고 이미지를 업로드하여 광고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="e5593-115">축소판 이미지와 광고 목록을 볼 수 있습니다 및 광고 toosee hello 세부 정보를 선택할 때 hello에 전체 이미지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![광고 목록](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="e5593-117">hello 응용 프로그램 hello를 사용 하 여 [큐 중심 작업 패턴](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff 부하 CPU를 많이 사용 hello 만드는 작업을 미리 보기 tooa 백 엔드 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="e5593-118">대체 아키텍처: 웹 사이트 및 WebJobs</span><span class="sxs-lookup"><span data-stu-id="e5593-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="e5593-119">이 자습서에서는 어떻게 toorun 프런트 엔드 및 백 엔드는 Azure에서 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="e5593-120">대신은 toorun hello에 프런트 엔드는 [Azure 웹 사이트](/services/web-sites/) hello를 사용 하 여 [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) hello 백 엔드에 대 한 (현재 미리 보기)의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="e5593-121">에서 WebJobs을 사용 하는 방법에 대 한 참조 [hello Azure WebJobs SDK 시작](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="e5593-122">시나리오에 적합 하는 방법을 toochoose hello 서비스를 가장 하는 방법에 대 한 정보를 참조 하세요. [Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교](../app-service-web/choose-web-site-cloud-service-vm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="e5593-123">학습할 내용</span><span class="sxs-lookup"><span data-stu-id="e5593-123">What you'll learn</span></span>
* <span data-ttu-id="e5593-124">어떻게 tooenable 시스템에 설치 하 여 Azure 개발 hello Azure SDK입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="e5593-125">어떻게 toocreate Visual Studio 클라우드 서비스 프로젝트는 ASP.NET MVC 웹 역할 및 작업자 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="e5593-126">어떻게 tootest 클라우드 서비스 프로젝트를 로컬로 hello Azure 저장소 에뮬레이터를 사용 하 여 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="e5593-127">어떻게 toopublish hello 클라우드 프로젝트 tooan Azure 클라우드 서비스와 Azure 저장소 계정을 사용 하 여 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="e5593-128">Tooupload 파일 방법과 hello Azure Blob 서비스에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="e5593-129">어떻게 toouse hello 계층 간 통신에 대 한 Azure 큐 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5593-130">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e5593-130">Prerequisites</span></span>
<span data-ttu-id="e5593-131">hello 자습서 알고 있다고 가정 [클라우드 서비스를 Azure에 대 한 기본 개념](cloud-services-choose-me.md) 같은 *웹 역할* 및 *작업자 역할* 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="e5593-132">또한 알고 있다고 가정 어떻게와 toowork [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) 또는 [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) Visual Studio의 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="e5593-133">hello 예제 응용 프로그램 MVC를 사용 하지만 tooWeb Forms 대부분의 hello 자습서에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="e5593-134">Azure 구독을 하지 않고 로컬 hello 앱을 실행할 수는 있지만 한 toodeploy hello 응용 프로그램 toohello 클라우드 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="e5593-135">계정이 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668)하거나 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="e5593-136">hello 자습서 지침은 hello 제품을 다음 중 하나로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="e5593-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="e5593-137">Visual Studio 2013</span></span>
* <span data-ttu-id="e5593-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e5593-138">Visual Studio 2015</span></span>
* <span data-ttu-id="e5593-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e5593-139">Visual Studio 2017</span></span>

<span data-ttu-id="e5593-140">다음 중 하나에 없을 경우 hello Azure SDK를 설치 하면 Visual Studio 자동으로 설치 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="e5593-141">응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="e5593-141">Application architecture</span></span>
<span data-ttu-id="e5593-142">hello 응용 프로그램을 Entity Framework Code First toocreate hello 테이블과 hello 데이터 액세스를 사용 하 여 SQL 데이터베이스에 광고를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="e5593-143">각 광고에 대 한 hello 데이터베이스 저장소 두 Url에 대 한 전체 크기 이미지와 hello 미리 보기에 대 한 하나의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![광고 테이블](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="e5593-145">사용자 이미지를 업로드 하면에 hello 이미지를 저장 웹 역할에서 프런트 엔드 실행 hello는 [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), toohello blob을 가리키는 URL 사용 하 여 hello 데이터베이스의 hello ad 정보를 저장 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="e5593-146">At hello 동일 time, 메시지 tooan Azure 큐를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="e5593-147">작업자 역할에서 정기적으로 실행 하는 백 엔드 프로세스는 새 메시지에 대 한 hello 큐를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="e5593-148">새 메시지가 표시 되 면 hello 작업자 역할을 만들고 해당 이미지에 대 한 미리 보기 하며 업데이트 hello 해당 ad에 대 한 축소판 그림 URL 데이터베이스 필드</span><span class="sxs-lookup"><span data-stu-id="e5593-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="e5593-149">hello 다음 그림에 hello 응용 프로그램의 hello 부분 어떻게 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Contoso Ads 아키텍처](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="e5593-151">다운로드 하 고 완료 하는 hello 솔루션 실행</span><span class="sxs-lookup"><span data-stu-id="e5593-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="e5593-152">다운로드 하 고 hello 압축을 풀면 [솔루션 완료](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="e5593-153">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="e5593-154">Hello에서 **파일** 메뉴 선택 **프로젝트 열기**hello 솔루션을 다운로드 한 toowhere 이동한 다음 hello 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="e5593-155">CTRL + SHIFT + B toobuild hello 솔루션 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="e5593-156">기본적으로 Visual Studio 자동으로 복원 hello에 포함 되지 않은 hello NuGet 패키지 콘텐츠를 *.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="e5593-157">Hello 패키지를 복원 하지 마십시오 하 여 수동으로 설치 거 toohello **솔루션에 대 한 NuGet 패키지 관리** hello를 클릭 하 고 대화 상자 **복원** hello 상단 오른쪽에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="e5593-158">**솔루션 탐색기**, 다음 사항을 확인 **ContosoAdsCloudService** hello 시작 프로젝트로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="e5593-159">Visual Studio 2015를 사용 하는 하거나 이상 hello 응용 프로그램에서 hello SQL Server 연결 문자열을 변경 *Web.config* hello ContosoAdsWeb 프로젝트의 파일과 hello에 *ServiceConfiguration.Local.cscfg* hello ContosoAdsCloudService 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="e5593-160">각각의 경우 "(localdb) \v11.0"를도 변경 "(localdb) \MSSQLLocalDB"입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="e5593-161">CTRL + f 5 toorun hello 응용 프로그램 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="e5593-162">클라우드 서비스 프로젝트를 로컬로 실행할 때 Visual Studio hello Azure에서 자동으로 호출 *계산 에뮬레이터* 및 Azure *저장소 에뮬레이터*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="e5593-163">hello는 컴퓨터의 리소스 toosimulate hello 웹 역할 및 작업자 역할 환경을 사용 하 여 에뮬레이터를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="e5593-164">사용 하 여 hello 저장소 에뮬레이터는 [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) 데이터베이스 toosimulate Azure 클라우드 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="e5593-165">hello 처음으로 클라우드 서비스 프로젝트를 실행 하면 걸리는 1 분 정도를 에뮬레이터 toostart hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="e5593-166">에뮬레이터 시작이 완료 되 면 hello 기본 브라우저 toohello 응용 프로그램 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Contoso Ads 아키텍처](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="e5593-168">**광고 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="e5593-169">테스트 데이터를 입력 하 고 선택 된 *.jpg* tooupload, 이미지 및 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![만들기 페이지](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="e5593-171">hello 앱 toohello 인덱스 페이지 까지일 처리 하는 아직 만들어지지 않은 때문에 새 ad hello에 대 한 미리 보기 표시 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="e5593-172">잠시 기다린 후 toosee hello 축소판 그림 hello 인덱스 페이지를 새로 고 치세요.</span><span class="sxs-lookup"><span data-stu-id="e5593-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![인덱스 페이지](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="e5593-174">클릭 **세부 정보** ad toosee hello 큰 이미지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![자세히 페이지](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="e5593-176">연결 toohello 클라우드가 없는 로컬 컴퓨터에서 전체 hello 응용 프로그램을 실행 했으므로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="e5593-177">hello 저장소 에뮬레이터 hello 큐를 저장 하 고 blob 데이터는 SQL Server Express LocalDB 데이터베이스 및 hello 응용 프로그램에 다른 LocalDB 데이터베이스의 hello ad 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="e5593-178">Entity Framework Code First 자동으로 만들어진된 hello ad 데이터베이스 hello 것 처음으로 hello 웹 앱 tooaccess 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="e5593-179">다음 섹션 hello hello 클라우드에서 실행 될 때 큐, blob 및 hello 응용 프로그램 데이터베이스에 대 한 hello 솔루션 toouse Azure 클라우드 리소스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="e5593-180">Toocontinue toorun 로컬로 려 해도 클라우드 저장소 및 데이터베이스 리소스를 사용할 경우에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="e5593-181">표시 하는 연결 문자열을 설정할 때의 문제만는 어떻게 toodo 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="e5593-182">Hello 응용 프로그램 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="e5593-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="e5593-183">작업 단계 toorun hello 응용 프로그램 hello 클라우드에서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="e5593-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="e5593-184">Azure 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="e5593-185">Azure SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="e5593-186">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e5593-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="e5593-187">Azure에서 실행 될 때 솔루션 toouse hello Azure SQL 데이터베이스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="e5593-188">Azure에서 실행 될 때 솔루션 toouse hello Azure 저장소 계정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="e5593-189">Hello 프로젝트 tooyour Azure 클라우드 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="e5593-190">Azure 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="e5593-190">Create an Azure cloud service</span></span>
<span data-ttu-id="e5593-191">Azure 클라우드 서비스는 hello 환경 hello 응용 프로그램에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="e5593-192">브라우저를 열고 hello [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e5593-193">**새로 만들기 > Compute > Cloud Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="e5593-194">Hello DNS 이름 입력된 상자에 hello 클라우드 서비스에 대 한 URL 접두사를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="e5593-195">이 URL에 고유한 toobe 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-195">This URL has toobe unique.</span></span>  <span data-ttu-id="e5593-196">선택한 hello 접두사는 이미 사용 하는 경우 오류 메시지가 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="e5593-197">Hello 서비스에 대 한 새 리소스 그룹을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="e5593-198">클릭 **새로 만들기** 다음 hello 리소스 그룹 입력된 상자에서 CS_contososadsRG 같은 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="e5593-199">Hello를 영역 toodeploy hello 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="e5593-200">이 필드는 클라우드 서비스가 호스팅될 데이터센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="e5593-201">프로덕션 응용 프로그램에 대 한 hello 지역 가장 가까운 tooyour 고객을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="e5593-202">이 자습서에 대 한 hello 지역 가장 가까운 tooyou를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="e5593-203">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-203">Click **Create**.</span></span>

    <span data-ttu-id="e5593-204">다음 이미지는 hello, 클라우드 서비스 URL CSvccontosoads.cloudapp.net hello로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![새 클라우드 서비스](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="e5593-206">Azure SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="e5593-206">Create an Azure SQL database</span></span>
<span data-ttu-id="e5593-207">Hello 앱 hello 클라우드에서 실행 되 면 클라우드 기반 데이터베이스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="e5593-208">Hello에 [Azure 포털](https://portal.azure.com), 클릭 **새로 만들기 > 데이터베이스 > SQL 데이터베이스**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="e5593-209">Hello에 **데이터베이스 이름** 상자에 입력 *contosoads*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="e5593-210">Hello에 **리소스 그룹**, 클릭 **기존 항목 사용** 및 hello 클라우드 서비스에 사용 되는 선택 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="e5593-211">Hello에서 이미지를 다음 클릭 **서버-필요한 설정 구성** 및 **새 서버 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![터널 toodatabase 서버](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="e5593-213">또는 이미 구독에는 서버가 있으면 해당 서버 hello 드롭 다운 목록에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="e5593-214">Hello에 **서버 이름** 상자에 입력 *csvccontosodbserver*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="e5593-215">관리자 **로그인 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="e5593-216">**새 서버 만들기**를 선택한 경우 여기에 기존 이름 및 암호를 입력하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="e5593-217">새 이름 및 암호를 정의 하는 이제 toouse 나중 hello 데이터베이스에 액세스할 때 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="e5593-218">이전에 만든 서버를 선택한 경우 이미 만든 hello 암호 toohello 관리 사용자 계정에 대 한 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="e5593-219">선택 동일 hello **위치** hello 클라우드 서비스에 대해 선택한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="e5593-220">Hello 클라우드 서비스와 데이터베이스가 서로 다른 데이터 센터에 있는 하는 경우 (지역), 지연이 증가할 및 hello 데이터 센터 외부 대역폭에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="e5593-221">데이터 센터 내부 대역폭은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="e5593-222">확인 **허용 azure 서비스 tooaccess 서버**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="e5593-223">클릭 **선택** hello 새 서버에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-223">Click **Select** for hello new server.</span></span>

    ![새 SQL Database 서버](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="e5593-225">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="e5593-226">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e5593-226">Create an Azure storage account</span></span>
<span data-ttu-id="e5593-227">Azure 저장소 계정을 hello 클라우드에서 큐 및 blob 데이터를 저장 하는 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="e5593-228">실제 응용 프로그램에서는 일반적으로 응용 프로그램 데이터와 로깅 데이터를 위한 별도의 계정 및 테스트 데이터와 프로덕션 데이터를 위한 별도의 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="e5593-229">이 자습서에서는 하나의 계정만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="e5593-230">Hello에 [Azure 포털](https://portal.azure.com), 클릭 **새로 만들기 > 저장소 > 저장소 계정-blob, 파일, 테이블, 큐**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="e5593-231">Hello에 **이름** 상자에 URL 접두사를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="e5593-232">이 접두사 이름과 함께 hello 텍스트 hello 상자 아래 hello 고유 URL tooyour 저장소 계정이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="e5593-233">다른 사용자가 입력 하는 hello 접두사를 이미 사용 하는 경우 해야 toochoose 접두사는 서로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="e5593-234">집합 hello **배포 모델** 너무*클래식*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="e5593-235">집합 hello **복제** 드롭 다운 목록 너무**로컬 중복 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="e5593-236">저장소 계정에 대 한 지리적 복제를 사용 하는 경우 저장 된 hello 콘텐츠인지 복제 tooa 보조 데이터 센터 tooenable 장애 조치 hello 기본 위치에서 중요 재해가 발생 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="e5593-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="e5593-237">지역에서 복제는 추가 비용을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="e5593-238">테스트 및 개발 계정에 대 한 일반적으로 원하지 toopay 지리적 복제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="e5593-239">자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제](../storage/common/storage-create-storage-account.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="e5593-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="e5593-240">Hello에 **리소스 그룹**, 클릭 **기존 항목 사용** 및 hello 클라우드 서비스에 사용 되는 선택 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="e5593-241">집합 hello **위치** 드롭 다운 목록 toohello hello 클라우드 서비스에 대해 선택한 동일한 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="e5593-242">Hello 클라우드 서비스와 저장소 계정이 서로 다른 데이터 센터가 있는 경우 (지역), 지연이 증가할 및 hello 데이터 센터 외부 대역폭에 대 한 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="e5593-243">데이터 센터 내부 대역폭은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="e5593-244">Azure 선호도 그룹 메커니즘 toominimize hello 거리 간의 대기 시간을 줄일 수 있는 데이터 센터의 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="e5593-245">이 자습서는 선호도 그룹을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="e5593-246">자세한 내용은 참조 [어떻게 tooCreate는 선호도 그룹을 Azure에서](http://msdn.microsoft.com/library/jj156209.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="e5593-247">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-247">Click **Create**.</span></span>

    ![새 저장소 계정](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="e5593-249">Hello 이미지에서 저장소 계정을 hello URL로 만든 `csvccontosoads.core.windows.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="e5593-250">Azure에서 실행 될 때 솔루션 toouse hello Azure SQL 데이터베이스 구성</span><span class="sxs-lookup"><span data-stu-id="e5593-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="e5593-251">웹 프로젝트 hello hello 작업자 역할 프로젝트 각각에 자체 데이터베이스 연결 문자열 및 Azure의 hello 응용 프로그램을 실행 하는 경우 toopoint toohello Azure SQL 데이터베이스 요구 각각.</span><span class="sxs-lookup"><span data-stu-id="e5593-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="e5593-252">사용 하 여 한 [f i g 변환](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) hello 웹 역할과 작업자 역할 hello에 대 한 클라우드 서비스 환경 설정에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="e5593-253">이 섹션 및 hello 다음 섹션에서는 프로젝트 파일에 자격 증명을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="e5593-254">[중요한 데이터를 공개 소스 코드 리포지토리에 저장하지 마세요](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)(영문).</span><span class="sxs-lookup"><span data-stu-id="e5593-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="e5593-255">Hello ContosoAdsWeb 프로젝트를 열고 hello *Web.Release.config* hello 응용 프로그램에 대 한 변환 파일 *Web.config* 파일을 포함 하는 hello 주석 블록을 삭제 한 `<connectionStrings>` 요소 및 붙여넣기 코드 대신에서 다음 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="e5593-256">Hello 파일을 편집 하기 위해 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="e5593-257">Hello에 [Azure 포털](https://portal.azure.com), 클릭 **SQL 데이터베이스** hello 왼쪽된 창에서이 자습서에서 만든 hello 데이터베이스를 클릭 한 다음 클릭 **연결 문자열 표시**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![연결 문자열 표시](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="e5593-259">hello 포털 hello 암호에 대 한 자리 표시자로의 연결 문자열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![연결 문자열](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="e5593-261">Hello에 *Web.Release.config* 변환 파일, 삭제 `{connectionstring}` 해당 위치 hello hello Azure 포털에서에서 ADO.NET 연결 문자열에에서 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="e5593-262">Hello에 붙여 넣은 hello 연결 문자열에 *Web.Release.config* 변환 파일, 대체 `{your_password_here}` hello 새 SQL 데이터베이스에 대해 만든 hello 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="e5593-263">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-263">Save hello file.</span></span>  
6. <span data-ttu-id="e5593-264">선택 하 고 hello 작업자 역할 프로젝트를 구성 하기 위한 단계를 수행 하는 hello에서 사용 하기 위해 (인용 부호를 둘러싼 hello) 없이 hello 연결 문자열을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="e5593-265">**솔루션 탐색기**아래 **역할** hello 클라우드 서비스 프로젝트에서 마우스 오른쪽 단추로 클릭 **ContosoAdsWorker** 클릭 하 고 **속성**.</span><span class="sxs-lookup"><span data-stu-id="e5593-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![역할 속성](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="e5593-267">Hello 클릭 **설정을** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="e5593-268">변경 **서비스 구성** 너무**클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="e5593-269">선택 hello **값** hello에 대 한 필드 `ContosoAdsDbConnectionString` 설정과 hello hello 자습서의 이전 섹션에서 복사한 hello 연결 문자열을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![작업자 역할의 데이터베이스 연결 문자열](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="e5593-271">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="e5593-272">Azure에서 실행 될 때 솔루션 toouse hello Azure 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="e5593-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="e5593-273">Hello 웹 역할 프로젝트와 hello 작업자 역할 프로젝트에 대 한 azure 저장소 계정 연결 문자열 hello 클라우드 서비스 프로젝트에서 환경 설정에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="e5593-274">각 프로젝트에 대해 별도 집합이 설정 toobe hello 응용 프로그램을 로컬로 실행 될 때 사용 하 고 hello 클라우드에서 실행 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="e5593-275">웹 및 작업자 역할 프로젝트에 대 한 hello 클라우드 환경 설정을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="e5593-276">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **ContosoAdsWeb** 아래 **역할** hello에 **ContosoAdsCloudService** 프로젝트를 마우스 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![역할 속성](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="e5593-278">Hello 클릭 **설정을** 탭 합니다. Hello에 **서비스 구성** 드롭다운 목록 상자에서 선택 **클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![클라우드 구성](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="e5593-280">선택 hello **StorageConnectionString** 항목을 확인할 수는 줄임표 (**...** ) hello 선의 hello 오른쪽 끝 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="e5593-281">Hello 줄임표 단추 tooopen hello 클릭 **저장소 계정 연결 문자열 만들기** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e5593-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![열린 연결 문자열 만들기 상자](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="e5593-283">Hello에 **저장소 연결 문자열 만들기** 대화 상자를 클릭 **구독**, 이전에 만든 hello 저장소 계정을 선택 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="e5593-284">아직 로그인하지 않은 경우 Azure 계정 자격 증명을 요구하는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![저장소 연결 문자열 만들기](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="e5593-286">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-286">Save your changes.</span></span>
6. <span data-ttu-id="e5593-287">다음과 같은 hello hello에 사용한 프로시저 `StorageConnectionString` 연결 문자열 tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="e5593-288">이 연결 문자열은 로깅에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="e5593-289">다음과 같은 hello hello에 사용한 프로시저 **ContosoAdsWeb** 역할 tooset hello에 대 한 연결 문자열 모두 **ContosoAdsWorker** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="e5593-290">Tooset 반드시 **서비스 구성** 너무**클라우드**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="e5593-291">Visual Studio UI hello를 사용 하 여 구성 해야 하는 hello 역할 환경 설정 hello hello ContosoAdsCloudService 프로젝트의 파일을 다음에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="e5593-292">*ServiceDefinition.csdef* -hello 설정 이름을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="e5593-293">*ServiceConfiguration.Cloud.cscfg* -hello 클라우드에서 hello 응용 프로그램을 실행 하는 경우에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="e5593-294">*ServiceConfiguration.Local.cscfg* -hello 앱 로컬로 실행 하는 경우에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="e5593-295">예를 들어 hello ServiceDefinition.csdef hello 정의 뒤에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="e5593-296">Hello 및 *ServiceConfiguration.Cloud.cscfg* Visual Studio에서 이러한 설정을 입력 한 hello 값을 포함 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="e5593-297">hello `<Instances>` 설정은 Azure에서 실행 되는 hello 작업자 역할 코드는 가상 컴퓨터의 hello 수를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="e5593-298">hello [다음 단계](#next-steps) 섹션에는 클라우드 서비스를 확장 하는 방법에 대 한 링크 toomore 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="e5593-299">Hello 프로젝트 tooAzure 배포</span><span class="sxs-lookup"><span data-stu-id="e5593-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="e5593-300">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello **ContosoAdsCloudService** 클라우드 프로젝트를 클릭 한 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![게시 메뉴](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="e5593-302">Hello에 **로그인** hello 단계의 **Azure 응용 프로그램 게시** 마법사를 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![로그인 단계](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="e5593-304">Hello에 **설정** 단계 hello 마법사의 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![설정 단계](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="e5593-306">hello에서 기본 설정을 hello **고급** 탭이이 자습서에 대 한 세밀 하 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="e5593-307">고급 탭 hello에 대 한 정보를 참조 하십시오. [Azure 응용 프로그램 게시 마법사](http://msdn.microsoft.com/library/hh535756.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="e5593-308">Hello에 **요약** 단계, 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-308">In hello **Summary** step, click **Publish**.</span></span>

    ![요약 단계](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="e5593-310">hello **Azure 활동 로그** 창이 Visual Studio에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="e5593-311">Hello 오른쪽 화살표 아이콘 tooexpand hello 배포 세부 정보를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="e5593-312">hello 배포 자세한 toocomplete 또는 too5 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Azure 활동 로그 창](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="e5593-314">Hello 배포 상태가 완료 되 면 클릭 hello **웹 앱 URL** toostart hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="e5593-315">이제 hello 응용 프로그램을 로컬로 실행할 때와 마찬가지로 만들기, 보기 및 일부 광고를 편집 하 여 hello 앱을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="e5593-316">때 테스트 탭, 삭제 또는 hello 클라우드 서비스 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="e5593-317">Hello 클라우드 서비스를 사용 하지 않는 경우에 가상 컴퓨터 리소스에 대 한 예약 되어 있으므로 요금이 발생 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="e5593-318">또한 실행 중인 채로 두는 경우에는 누군가가 URL을 발견하면 광고를 만들고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="e5593-319">Hello에 [Azure 포털](https://portal.azure.com), toohello 이동 **개요** 탭 클라우드 서비스를 클릭 한 다음 hello **삭제** hello hello 페이지 위쪽에 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="e5593-320">Tootemporarily 방지 다른 원한다 면 hello 사이트에 액세스할 수 없게, 클릭 **중지** 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="e5593-321">이 경우 요금이 tooaccrue를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="e5593-322">유사한 프로시저 toodelete hello SQL 데이터베이스 및 저장소 계정을 더 이상 필요할 때 따를 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="e5593-323">처음부터 hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e5593-323">Create hello application from scratch</span></span>
<span data-ttu-id="e5593-324">아직 다운로드 하지 않은 경우 [완료 hello 응용 프로그램](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)를 지금 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="e5593-325">Hello 새 프로젝트로 hello 다운로드 한 프로젝트에서 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="e5593-326">Hello Contoso 광고 응용 프로그램을 만드는 단계를 수행 하는 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="e5593-327">클라우드 서비스 Visual Studio 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="e5593-328">NuGet 패키지를 업데이트 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="e5593-329">프로젝트 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-329">Set project references.</span></span>
* <span data-ttu-id="e5593-330">연결 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-330">Configure connection strings.</span></span>
* <span data-ttu-id="e5593-331">코드 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-331">Add code files.</span></span>

<span data-ttu-id="e5593-332">Hello 솔루션을 만든 후에 고유 toocloud 서비스 프로젝트 및 Azure blob 및 큐를 hello 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="e5593-333">클라우드 서비스 Visual Studio 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="e5593-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="e5593-334">Visual Studio에서 선택 **새 프로젝트** hello에서 **파일** 메뉴.</span><span class="sxs-lookup"><span data-stu-id="e5593-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="e5593-335">Hello hello의 왼쪽된 창에서 **새 프로젝트** 대화 상자에서 **Visual C#** 선택 **클라우드** 템플릿 hello 선택 **Azure클라우드서비스** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="e5593-336">Hello 프로젝트 및 솔루션 ContosoAdsCloudService, 이름을 지정 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![새 프로젝트](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="e5593-338">Hello에 **새 Azure 클라우드 서비스** 대화 상자에서 웹 역할과 작업자 역할을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="e5593-339">Hello 웹 역할 ContosoAdsWeb, 이름을 지정 하 고 hello 작업자 역할 ContosoAdsWorker 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="e5593-340">(Hello 역할 hello 오른쪽 창 toochange hello 기본 이름에 hello 연필 아이콘을 사용 합니다.)</span><span class="sxs-lookup"><span data-stu-id="e5593-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![새 클라우드 서비스 프로젝트](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="e5593-342">Hello 표시 되 면 **새 ASP.NET 프로젝트** hello 웹 역할에 대 한 대화 상자 hello MVC 템플릿을 선택한 다음를 클릭 한 다음 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![인증 변경](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="e5593-344">Hello에 **인증 변경** 대화 상자에서 선택 **인증 안 함**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![인증 없음](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="e5593-346">Hello에 **새 ASP.NET 프로젝트** 대화 상자를 클릭 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="e5593-347">**솔루션 탐색기**(중 하나가 아닙니다 hello 프로젝트), hello 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **추가-새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="e5593-348">Hello에 **새 프로젝트 추가** 대화 상자에서 선택 **Windows** 아래 **Visual C#** 왼쪽된 창의 hello와 hello 클릭 **클래스 라이브러리** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="e5593-349">이름 hello 프로젝트 *ContosoAdsCommon*, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="e5593-350">Tooreference hello Entity Framework 컨텍스트 및 hello 데이터 모델은 웹 및 작업자 역할 프로젝트에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="e5593-351">대신 hello 웹 역할 프로젝트에 hello EF 관련 클래스를 정의 하 고 hello 작업자 역할 프로젝트에서 해당 프로젝트를 참조할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="e5593-352">하지만 다른 방법인 hello 작업자 역할 프로젝트 참조 tooweb 어셈블리 필요 하지 않습니다는.</span><span class="sxs-lookup"><span data-stu-id="e5593-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="e5593-353">NuGet 패키지 업데이트 및 추가</span><span class="sxs-lookup"><span data-stu-id="e5593-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="e5593-354">열기 hello **NuGet 패키지 관리** hello 솔루션에 대 한 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="e5593-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="e5593-355">Hello 창의 hello 위쪽 선택 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="e5593-356">Hello에 대 한 확인 *WindowsAzure.Storage* 패키지 및 hello 목록에 있으면 선택한 선택 hello 웹 및 작업자 프로젝트 tooupdate에서 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="e5593-357">hello 저장소 클라이언트 라이브러리는 Visual Studio 프로젝트 템플릿 보다 더 자주 업데이트 됩니다 업데이트 새로 만든 프로젝트 요구 toobe에서 종종 해당 hello 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="e5593-358">Hello 창의 hello 위쪽 선택 **찾아보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="e5593-359">Hello *EntityFramework* NuGet 패키지를 선택한 세 프로젝트 모두에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="e5593-360">Hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet 패키지 및 hello 작업자 역할 프로젝트에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="e5593-361">프로젝트 참조 설정</span><span class="sxs-lookup"><span data-stu-id="e5593-361">Set project references</span></span>
1. <span data-ttu-id="e5593-362">Hello ContosoAdsWeb 프로젝트 참조 toohello ContosoAdsCommon 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="e5593-363">Hello ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 누른 **참조** - **참조 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="e5593-364">Hello에 **참조 관리자** 대화 상자에서 **등 프로젝트 솔루션** hello 왼쪽된 창에서 선택 **ContosoAdsCommon**, 클릭 하 고 **확인**.</span><span class="sxs-lookup"><span data-stu-id="e5593-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="e5593-365">Hello ContosoAdsWorker 프로젝트 참조 toohello ContosAdsCommon 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="e5593-366">ContosoAdsCommon은 hello Entity Framework 데이터 모델 및 컨텍스트 클래스를 사용해 프런트 엔드 및 백 엔드 모두 hello 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="e5593-367">Hello ContosoAdsWorker 프로젝트에 대 한 참조를 너무 설정`System.Drawing`합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="e5593-368">이 어셈블리는 hello 백 엔드 tooconvert 이미지 toothumbnails에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="e5593-369">연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="e5593-369">Configure connection strings</span></span>
<span data-ttu-id="e5593-370">이 섹션에서는 로컬 테스트를 위해 Azure Storage 및 SQL 연결 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="e5593-371">hello 자습서의 앞부분에 나오는 hello 배포 지침 hello 응용 프로그램에서에서 실행 되 면 hello 클라우드 tooset hello 연결에 대 한 문자열 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="e5593-372">Hello ContosoAdsWeb 프로젝트, 열기 hello 응용 프로그램 Web.config 파일 및 insert hello 다음에 `connectionStrings` hello 다음 요소의 `configSections` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="e5593-373">Visual Studio 2015 이상을 사용하는 경우 "v11.0"을 "MSSQLLocalDB"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="e5593-374">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-374">Save your changes.</span></span>
3. <span data-ttu-id="e5593-375">Hello ContosoAdsCloudService 프로젝트 ContosoAdsWeb 아래에서 마우스 오른쪽 단추로 클릭 **역할**, 클릭 하 고 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![역할 속성](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="e5593-377">Hello에 **ContosAdsWeb [역할]** 속성 창의 hello 클릭 **설정** 탭을 클릭 한 다음 **설정 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="e5593-378">둡니다 **서비스 구성** 도**모든 구성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="e5593-379">이름이 *StorageConnectionString*인 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="e5593-380">설정 **형식** 너무*ConnectionString*, 설정 및 **값** 너무*UseDevelopmentStorage = true*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![새 연결 문자열](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="e5593-382">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-382">Save your changes.</span></span>
7. <span data-ttu-id="e5593-383">에 따라 동일한 프로시저 tooadd hello ContosoAdsWorker 역할 속성에는 저장소 연결 문자열을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="e5593-384">Hello에 여전히 **ContosoAdsWorker [역할]** 속성 창 다른 연결 문자열을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="e5593-385">이름: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="e5593-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="e5593-386">형식: String</span><span class="sxs-lookup"><span data-stu-id="e5593-386">Type: String</span></span>
   * <span data-ttu-id="e5593-387">값: 붙여넣기 hello 동일 hello 웹 역할 프로젝트에 대해 사용 된 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="e5593-388">(다음 예제는 hello Visual Studio 2013 용입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="e5593-389">잊지 마십시오 toochange hello 데이터 원본을이 예제를 복사 하 고 Visual Studio 2015 이상이 사용 하는 경우.)</span><span class="sxs-lookup"><span data-stu-id="e5593-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="e5593-390">코드 파일 추가</span><span class="sxs-lookup"><span data-stu-id="e5593-390">Add code files</span></span>
<span data-ttu-id="e5593-391">이 섹션에서는 hello 새 솔루션에 다운로드 한 hello 솔루션에서 코드 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="e5593-392">hello 다음 섹션에서는 표시 되며이 코드의 주요 부분에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="e5593-393">tooadd 파일 tooa 프로젝트 또는 폴더, 마우스 오른쪽 단추로 클릭 hello 프로젝트 또는 폴더와 클릭 **추가** - **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="e5593-394">Hello 파일을 클릭 한 다음 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="e5593-395">기존 파일 tooreplace 사용할지 요청 되 면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="e5593-396">Hello ContosoAdsCommon 프로젝트에서 삭제 hello *Class1.cs* 파일을 해당 위치 hello에 추가할 *Ad.cs* 및 *ContosoAdscontext.cs* hello에서 파일 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="e5593-397">Hello ContosoAdsWeb 프로젝트 hello 파일 다운로드 hello 프로젝트에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="e5593-398">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="e5593-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="e5593-399">Hello에 *Views\Shared* 폴더:  *\_Layout.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="e5593-400">Hello에 *Views\Home* 폴더: *Index.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="e5593-401">Hello에 *컨트롤러* 폴더: *AdController.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="e5593-402">Hello에 *Views\Ad* 폴더 (먼저 hello 폴더 만들기): 5 *.cshtml* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="e5593-403">Hello ContosoAdsWorker 프로젝트에서 추가 *WorkerRole.cs* hello에서 프로젝트를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="e5593-404">이제 작성 하 고 hello 자습서의 앞부분에서 설명 된 대로 hello 응용 프로그램을 실행할 수 있습니다 및 로컬 데이터베이스 및 저장소 에뮬레이터 리소스가 hello 앱 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="e5593-405">hello 다음 섹션에서는 코드를 설명 hello Azure 환경, blob 및 큐와 관련된 tooworking hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="e5593-406">이 자습서에서는 설명 하지 않습니다 어떻게 toocreate MVC 컨트롤러 및 뷰를 스 캐 폴딩을 사용 하 여, toowrite Entity Framework 코드를 어떤 방식으로 SQL Server 데이터베이스 또는 ASP.NET 4.5에 비동기 프로그래밍의 hello 기본 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="e5593-407">이러한 항목에 대 한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="e5593-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="e5593-408">MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="e5593-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="e5593-409">EF 6 및 MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="e5593-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="e5593-410">[.NET 4.5에서 tooasynchronous 프로그래밍 소개](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="e5593-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="e5593-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="e5593-412">hello Ad.cs 파일 ad 범주에 대 한 enum과 ad 정보에 대 한 POCO 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
public enum Category
{
    Cars,
    [Display(Name="Real Estate")]
    RealEstate,
    [Display(Name = "Free Stuff")]
    FreeStuff
}

public class Ad
{
    public int AdId { get; set; }

    [StringLength(100)]
    public string Title { get; set; }

    public int Price { get; set; }

    [StringLength(1000)]
    [DataType(DataType.MultilineText)]
    public string Description { get; set; }

    [StringLength(1000)]
    [DisplayName("Full-size Image")]
    public string ImageURL { get; set; }

    [StringLength(1000)]
    [DisplayName("Thumbnail")]
    public string ThumbnailURL { get; set; }

    [DataType(DataType.Date)]
    [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
    public DateTime PostedDate { get; set; }

    public Category? Category { get; set; }
    [StringLength(12)]
    public string Phone { get; set; }
}
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="e5593-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="e5593-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="e5593-414">hello ContosoAdsContext 클래스 hello Ad 클래스 Entity Framework는 SQL 데이터베이스에 저장 하는 DbSet 컬렉션에 사용 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
public class ContosoAdsContext : DbContext
{
    public ContosoAdsContext() : base("name=ContosoAdsContext")
    {
    }
    public ContosoAdsContext(string connString)
        : base(connString)
    {
    }
    public System.Data.Entity.DbSet<Ad> Ads { get; set; }
}
```

<span data-ttu-id="e5593-415">hello 클래스에 두 명의 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-415">hello class has two constructors.</span></span> <span data-ttu-id="e5593-416">먼저 hello 그중에서 hello 웹 프로젝트에서 사용 하 고 hello Web.config 파일에 저장 된 연결 문자열의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="e5593-417">hello 두 번째 생성자 Web.config 파일 없으므로 hello 작업자 역할 프로젝트에서 사용 하는 hello 실제 연결 문자열에 toopass가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="e5593-418">했 듯이 여기서이 연결 문자열 저장 된 하 고 hello DbContext 클래스를 인스턴스화할 때 hello 코드 hello 연결 문자열을 검색 하는 어떻게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="e5593-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="e5593-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="e5593-420">Hello에서 호출 되는 코드 `Application_Start` 메서드 만듭니다는 *이미지* blob 컨테이너 및 *이미지* 아직 없는 경우 큐에 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="e5593-421">이렇게 하는 새 저장소 계정을 사용 하 여 시작 하거나 hello 저장소 에뮬레이터를 사용 하 여 새 컴퓨터에서 시작 때마다 hello 필요한 blob 컨테이너 및 큐가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="e5593-422">코드 가져옵니다 액세스 toohello 저장소 계정에서 hello hello 저장소 연결 문자열을 사용 하 여 hello *.cscfg* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="e5593-423">그런 다음 참조 toohello 가져오고 *이미지* blob 컨테이너, 존재 하지 않는 액세스 hello 새 컨테이너에 대 한 권한을 설정 하는 경우 hello 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="e5593-424">기본적으로 새 컨테이너 스토리지 계정으로 클라이언트를 자격 증명 tooaccess blob만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="e5593-425">hello 웹 사이트 지점 toohello 이미지 blob에 해당 Url을 사용 하 여 이미지를 표시할 수 있도록 blob toobe 공개를 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="e5593-426">비슷한 코드 참조 toohello 가져옵니다 *이미지* 대기 및 새 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="e5593-427">이런 경우 권한을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="e5593-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="e5593-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="e5593-429">hello *_Layout.cshtml* 파일 hello 머리글 및 바닥글에 hello 응용 프로그램 이름을 설정 하 고 "광고" 메뉴 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="e5593-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="e5593-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="e5593-431">hello *Views\Home\Index.cshtml* 파일 hello 홈 페이지에서 범주 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="e5593-432">hello의 hello 정수 값을 전달 하는 hello 링크 `Category` 쿼리 문자열 변수 toohello 광고 인덱스 페이지에는 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="e5593-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="e5593-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="e5593-434">Hello에 *AdController.cs* 파일, hello 생성자 호출 hello `InitializeStorage` blob 및 큐를 사용 하기 위한 API를 제공 하는 메서드 toocreate Azure 저장소 클라이언트 라이브러리 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="e5593-435">Hello 코드 참조 toohello 가져옵니다 다음 *이미지* 에서 이전에 본 것 처럼 컨테이너 blob *Global.asax.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="e5593-436">그 과정에서 웹앱에 해당하는 기본 [재시도 정책](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) (영문)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="e5593-437">hello 기본 지 수 백오프 재시도 정책을 일시적인 오류에 대 한 여러 번 시도에 1 분 보다 오랫동안 hello 웹 응용 프로그램 작동을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="e5593-438">여기에 지정 된 hello 재시도 정책을 toothree 시도를 각 시도 후 3 초 동안 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="e5593-439">비슷한 코드 참조 toohello 가져옵니다 *이미지* 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="e5593-440">대부분의 hello 컨트롤러 코드는 DbContext 클래스를 사용 하 여 Entity Framework 데이터 모델을 사용 하기 위한 일반적인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="e5593-441">예외는 hello HttpPost `Create` 메서드 파일을 업로드 하 고 blob 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="e5593-442">hello 모델 바인더를 제공는 [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello 메서드 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="e5593-443">Hello 사용자 파일 tooupload를 선택 하는 경우 hello 코드는 hello 파일을 업로드 하는 blob에 저장 및 toohello blob을 가리키는 URL로 hello Ad 데이터베이스 레코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="e5593-444">hello 코드 업로드 hello지 않습니다 하는 hello `UploadAndSaveBlobAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e5593-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="e5593-445">Hello blob, 업로드 및 저장 hello 파일에 대 한 GUID 이름을 만들고 참조 toohello 저장 된 blob를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
{
    string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
    CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
    using (var fileStream = imageFile.InputStream)
    {
        await imageBlob.UploadFromStreamAsync(fileStream);
    }
    return imageBlob;
}
```

<span data-ttu-id="e5593-446">Hello HttpPost 후 `Create` blob을 업로드 하는 메서드 및 업데이트 hello 데이터베이스, 해당 백 엔드 프로세스 이미지는 변환 tooa 축소판 그림에 대 한 준비 큐 메시지 tooinform 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="e5593-447">HttpPost hello에 대 한 코드 hello `Edit` 메서드는 점을 제외 하 고 hello 사용자가 새 이미지 파일을 선택 하는 경우 이미 존재 하는 모든 blob을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="e5593-448">다음 예제에서는 hello 광고를 삭제 하면 blob을 삭제 하는 hello 코드를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
private async Task DeleteAdBlobsAsync(Ad ad)
{
    if (!string.IsNullOrWhiteSpace(ad.ImageURL))
    {
        Uri blobUri = new Uri(ad.ImageURL);
        await DeleteAdBlobAsync(blobUri);
    }
    if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
    {
        Uri blobUri = new Uri(ad.ThumbnailURL);
        await DeleteAdBlobAsync(blobUri);
    }
}
private static async Task DeleteAdBlobAsync(Uri blobUri)
{
    string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
    CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
    await blobToDelete.DeleteAsync();
}
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="e5593-449">ContosoAdsWeb - Views\Ad\Index.cshtml 및 Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="e5593-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="e5593-450">hello *Index.cshtml* 파일 축소판 그림 hello로 다른 ad 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="e5593-451">hello *Details.cshtml* 파일 hello에 전체 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="e5593-452">ContosoAdsWeb - Views\Ad\Create.cshtml 및 Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="e5593-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="e5593-453">hello *Create.cshtml* 및 *Edit.cshtml* 파일 인코딩을 hello 컨트롤러 tooget hello를 사용 하도록 설정 하는 폼은 지정 `HttpPostedFileBase` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="e5593-454">`<input>` 요소 파일 선택 대화 상자 hello 브라우저 tooprovide 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="e5593-455">ContosoAdsWorker - WorkerRole.cs - OnStart 메서드</span><span class="sxs-lookup"><span data-stu-id="e5593-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="e5593-456">hello Azure 작업자 역할 환경 호출 hello `OnStart` hello에 대 한 메서드 `WorkerRole` hello 작업자 역할을 시작 하기 hello를 호출 하는 경우 클래스 `Run` 메서드 때 hello `OnStart` 메서드가 완료 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="e5593-457">hello `OnStart` 메서드 hello에서 hello 데이터베이스 연결 문자열을 가져옵니다 *.cscfg* 파일을 toohello 엔터티 프레임 워크 DbContext 클래스를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="e5593-458">hello 공급자가 지정 된 toobe 않아도 되므로 hello SQLClient 공급자는 기본적으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="e5593-459">그 후 hello 메서드 참조 toohello 저장소 계정을 가져옵니다 하 고 없는 경우 hello blob 컨테이너 및 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="e5593-460">에 대 한 hello 코드는 hello 웹 역할에서 이미 살펴본 비슷한 toowhat `Application_Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e5593-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="e5593-461">ContosoAdsWorker - WorkerRole.cs - Run 메서드</span><span class="sxs-lookup"><span data-stu-id="e5593-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="e5593-462">hello `Run` 메서드는 hello `OnStart` 메서드가 초기화 작업을 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="e5593-463">hello 메서드는 새 큐 메시지를 감시 하 고 도착 했을 때 처리 하는 무한 루프를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="e5593-464">Hello 루프를 반복할 때마다 큐 메시지가 없는 경우 hello 프로그램 초 동안 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="e5593-465">이렇게 하면 hello 작업자 역할을에서 과도 한 CPU 시간과 저장소 트랜잭션 비용을 발생 시 키 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="e5593-466">Microsoft 고객 자문 팀 hello tooproduction를 배포 하 고 휴가 용으로 남겨 둔는 개발자에 게이 tooinclude 찾기에 대 한 이야기를 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="e5593-467">그 얻었습니다 때 자신의 감독에 비해 hello 휴가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="e5593-468">경우에 따라 큐 메시지의 hello 콘텐츠 처리에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="e5593-469">이 라고는 *포이즌 메시지*, 방금 오류를 기록 하 고 hello 루프를 다시 시작을 시도할 수 있습니다 머무르면서 tooprocess 해당 메시지와 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="e5593-470">따라서 hello catch 블록이 포함 if 문을 toosee를 확인 하는 hello 앱 tooprocess 시도한 횟수 hello 현재 메시지 및 경과 했는데도 문제가 있다면 5 번 이상, hello 메시지 hello 큐에서 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="e5593-471">큐 메시지가 발견되는 경우 `ProcessQueueMessage`이(가) 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="e5593-472">이 코드 hello 데이터베이스 tooget hello 이미지 URL을 읽고, hello 이미지 tooa 축소판 그림으로 변환, blob의 hello 축소판 그림을 저장, hello 축소판 blob URL으로 hello 데이터베이스를 업데이트 및 hello 큐 메시지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="e5593-473">hello에 대 한 코드 hello `ConvertImageToThumbnailJPG` 메서드는 편의상 hello System.Drawing 네임 스페이스의 클래스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="e5593-474">그러나이 네임 스페이스의 hello 클래스는 Windows Forms 사용 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="e5593-475">Windows 또는 ASP.NET 서비스에서 사용할 수 있도록 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="e5593-476">이미지 처리 옵션에 대한 자세한 내용은 [동적 이미지 생성](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) 및 [이미지 크기 조정 세부 정보](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5593-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="e5593-477">문제 해결</span><span class="sxs-lookup"><span data-stu-id="e5593-477">Troubleshooting</span></span>
<span data-ttu-id="e5593-478">다음은 몇 가지 일반적인 오류가이 자습서에서는 hello 지침을 따라 하는 동안, 작동 하지 않는 경우와 방법을 tooresolve 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="e5593-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="e5593-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="e5593-480">hello `RoleEnvironment` 개체 hello Azure 계산 에뮬레이터를 사용 하 여 로컬로 실행 하는 경우 또는 Azure에서 응용 프로그램을 실행 하면 Azure에서 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="e5593-481">을 로컬로 실행 하는 경우이 오류를 발생 hello 시작 프로젝트로 hello ContosoAdsCloudService 프로젝트를 설정 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="e5593-482">이 hello 프로젝트 toorun hello Azure 계산 에뮬레이터를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="e5593-483">Hello에 저장 되어 있는 tooget hello 연결 문자열 값은 hello 응용 프로그램에서는 hello에 대 한 Azure RoleEnvironment hello 중 하나가 *.cscfg* 파일,이 예외는 누락 된 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="e5593-484">Hello ContosoAdsWeb 프로젝트에서 클라우드 모두에 대 한 hello StorageConnectionString 설정 및 구성을 로컬를 생성 하 여 두 구성 모두에 대 한 연결 문자열 모두 hello ContosoAdsWorker 프로젝트에서 만든 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="e5593-485">이렇게 하면 한 **모두 찾기** 검색 hello 전체 솔루션에서 StorageConnectionString에 대 한 표시 되어야 것 9 번 6 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="e5593-486">Tooport xxx를 재정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="e5593-487">프로토콜 http에 대한 최소 허용 값 8080 미만의 새 포트</span><span class="sxs-lookup"><span data-stu-id="e5593-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="e5593-488">Hello 웹 프로젝트에서 사용 하는 hello 포트 번호를 변경해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="e5593-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="e5593-489">Hello ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 누른 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="e5593-490">Hello 클릭 **웹** 탭을 선택한 다음 hello에 hello 포트 번호를 변경 **프로젝트 Url** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="e5593-491">Hello 문제를 해결할 수 있는 또 다른 방법은 hello 다음 섹션을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e5593-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="e5593-492">로컬 실행 중 다른 오류</span><span class="sxs-lookup"><span data-stu-id="e5593-492">Other errors when running locally</span></span>
<span data-ttu-id="e5593-493">새로운 클라우드 기본적으로 서비스 프로젝트는 hello Azure compute emulator express toosimulate hello Azure 환경을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="e5593-494">Hello 전체 계산 에뮬레이터의 경량 버전 이므로 일부 조건 hello에서 전체 에뮬레이터 hello express 버전에는 없는 될 때 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="e5593-495">toochange 프로젝트 toouse hello 전체 에뮬레이터 hello hello ContosoAdsCloudService 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="e5593-496">Hello에 **속성** 창을 클릭 hello **웹** 탭을 클릭 한 다음 hello **전체 에뮬레이터 사용** 라디오 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="e5593-497">주문 toorun hello 응용 프로그램 hello 전체 에뮬레이터와 함께 관리자 권한으로 Visual Studio tooopen을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5593-498">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e5593-498">Next steps</span></span>
<span data-ttu-id="e5593-499">Contoso 광고 응용 프로그램 hello 의도적으로 유지 하는 간단한-시작 자습서에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="e5593-500">예를 들어, 구현 하지 않습니다 [종속성 주입](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) 또는 hello [리포지토리와의 단위 작업 패턴](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), 그렇지 않은 [로깅에 대 한 인터페이스를 사용 하 여](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), 를사용하지않습니다[ EF Code First 마이그레이션을](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage 데이터 모델이 변경 또는 [EF 연결 복원 력](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage 일시적인 네트워크 오류, 및 등입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="e5593-501">다음은 더 많은 실제 코딩 관행을 복잡 한 덜 복잡 한 toomore에서 나열 된는 방법을 보여 주는 몇 가지 클라우드 서비스 샘플 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="e5593-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31)(영문).</span><span class="sxs-lookup"><span data-stu-id="e5593-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="e5593-503">개념상 비슷하지만 tooContoso 광고 하지만 더 많은 기능 및 구현 더 많은 실제 코딩 방법을 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="e5593-504">[테이블, 큐 및 Blob이 포함된 Azure 클라우드 서비스 다중 계층 응용 프로그램](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36)(영문).</span><span class="sxs-lookup"><span data-stu-id="e5593-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="e5593-505">Azure 저장소 테이블 뿐만 아니라 Blob 및 큐를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="e5593-506">.NET 용 hello Azure SDK의 이전 버전에 따라, 일부 수정 toowork hello 현재 버전으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="e5593-507">[Microsoft Azure의 클라우드 서비스 기본 사항(영문)](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="e5593-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="e5593-508">다양 한 범위의 hello Microsoft Patterns and Practices 그룹에 의해 생성 되는 모범 사례를 보여 주는 포괄적인 샘플입니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="e5593-509">Hello 클라우드에 대 한 개발에 대 한 일반 정보를 참조 하십시오. [Azure로 실제 클라우드 응용 프로그램 빌딩](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="e5593-510">한 비디오 지침은 tooAzure 저장소에 대 한 모범 사례 및 패턴, 참조 [Microsoft Azure 저장소 – 새로 만들기, 모범 사례 및 패턴 이란](http://channel9.msdn.com/Events/Build/2014/3-628)합니다.</span><span class="sxs-lookup"><span data-stu-id="e5593-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="e5593-511">자세한 내용은 다음 리소스는 hello 참조:</span><span class="sxs-lookup"><span data-stu-id="e5593-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="e5593-512">Azure 클라우드 서비스 1 부:</span><span class="sxs-lookup"><span data-stu-id="e5593-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="e5593-513">Toomanage 클라우드 서비스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e5593-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="e5593-514">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="e5593-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="e5593-515">어떻게 toochoose는 클라우드 서비스 공급자</span><span class="sxs-lookup"><span data-stu-id="e5593-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
