---
title: "Azure 앱 서비스의.NET WebJob aaaCreate | Microsoft Docs"
description: "ASP.NET MVC 및 Azure를 사용하여 다중 계층 앱을 만듭니다. hello Azure 앱 서비스의 웹 앱에 프런트 엔드가 실행 되 고 백 엔드가 실행 되는 WebJob으로 hello 합니다. hello 앱 Entity Framework, SQL 데이터베이스 및 Azure 저장소 큐 및 blob를 사용합니다."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="85c11-105">Azure 앱 서비스에서 .NET WebJob 만들기</span><span class="sxs-lookup"><span data-stu-id="85c11-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="85c11-106">이 자습서에서는 toowrite hello를 사용 하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 대 한 코드 하는 방법을 보여 줍니다. [WebJobs SDK](websites-dotnet-webjobs-sdk.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="85c11-107">hello의 목적은 hello [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello 코드가 예: 이미지 처리, 처리 큐, RSS 집계, 파일 유지 관리 같은 웹 작업이 수행할 수 있는 일반적인 작업에 대해 작성 되 고 전자 메일 보내기.</span><span class="sxs-lookup"><span data-stu-id="85c11-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="85c11-108">hello WebJobs SDK는 Azure 저장소 및 서비스 버스 작업을 위한, 작업을 예약 하 고 오류를 처리 및 기타 여러 가지 일반적인 시나리오에 대 한 기본 제공 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="85c11-109">또한에 toobe, 확장 가능한 설계 되어 있으므로 [확장에 대 한 오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="85c11-110">hello 샘플 응용 프로그램에는 광고 게시판입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="85c11-111">사용자가 광고에 대 한 이미지를 업로드할 수 하 고 백 엔드 프로세스 hello 이미지 toothumbnails를 변환 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="85c11-112">hello ad 목록 페이지 hello 미리 보기, 보여주며 hello ad 세부 정보 페이지에는 hello에 전체 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="85c11-113">다음 스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c11-113">Here's a screenshot:</span></span>

![광고 목록](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="85c11-115">이 샘플 응용 프로그램은 [Azure 큐](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 및 [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="85c11-116">hello 자습서에서는 어떻게 toodeploy hello 응용 프로그램 너무[Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) 및 [Azure SQL 데이터베이스](http://msdn.microsoft.com/library/azure/ee336279)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="85c11-117"><a id="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="85c11-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="85c11-118">hello 자습서 알고 있다고 가정 어떻게와 toowork [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) Visual Studio의 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="85c11-119">hello 자습서 Visual Studio 2013 용 쓰 였 있지만 이후 버전의 Visual Studio 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="85c11-120">Visual Studio 2015 또는 2017을 사용 하는 경우 확인 hello 응용 프로그램을 로컬로 실행 하기 전에 hello 변경 해야 `Data Source` hello hello Web.config 및 App.config 파일에서 SQL Server LocalDB 연결 문자열의 일부로 `Data Source=(localdb)\v11.0` 너무`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="85c11-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="85c11-121"><a name="note"></a>이 자습서는 Azure 계정 toocomplete이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="85c11-122">할 수 있습니다 [무료로 Azure 계정을 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): Azure 서비스를 유료 아웃 tootry 사용할 수 있으며 hello 계정을 유지 하 고 웹 사이트와 같은 무료 Azure 서비스를 사용 하 여 수 사용 하는 후에 크레딧을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="85c11-123">명시적으로 설정을 변경 하 고 청구 toobe 요청 하지 않는 한 신용 카드, 청구 됩니다 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="85c11-124">[Visual Studio 구독자에 대한 월별 Azure 크레딧을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="85c11-125">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="85c11-126">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="85c11-127"><a id="learn"></a>학습할 내용</span><span class="sxs-lookup"><span data-stu-id="85c11-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="85c11-128">hello 자습서 toodo hello 다음 작업 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="85c11-129">(에 Visual Studio 2013 및 2015 사용자) hello Azure SDK를 설치 하 여 Azure 개발을 위해 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="85c11-130">Hello 연결 된 웹 프로젝트를 배포할 때 Azure WebJob으로 자동으로 배포 하는 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="85c11-131">Hello 개발 컴퓨터에서 로컬로 WebJobs SDK 백 엔드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="85c11-132">앱 서비스에서 WebJobs 백 엔드 tooa 웹 앱과 응용 프로그램을 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="85c11-133">파일을 업로드 하 고 hello Azure Blob 서비스에에서 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="85c11-134">Azure 저장소 큐 및 blob와 Azure WebJobs SDK toowork hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="85c11-135"><a id="contosoads"></a>응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="85c11-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="85c11-136">hello 예제 응용 프로그램 사용 hello [큐 중심 작업 패턴](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff 부하 CPU를 많이 사용 hello 만드는 작업을 미리 보기 tooa 백 엔드 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="85c11-137">hello 응용 프로그램을 Entity Framework Code First toocreate hello 테이블과 hello 데이터 액세스를 사용 하 여 SQL 데이터베이스에 광고를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="85c11-138">각 광고에 대 한 hello 데이터베이스에는 두 개의 Url이는 저장: hello 전체 크기 이미지 hello 축소판 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![광고 테이블](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="85c11-140">hello 이미지를 저장 하는 사용자 이미지, hello 웹 앱을 업로드 하는 경우는 [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), toohello blob을 가리키는 URL 사용 하 여 hello 데이터베이스의 hello ad 정보를 저장 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="85c11-141">At hello 동일 time, 메시지 tooan Azure 큐를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="85c11-142">Azure WebJob으로 실행 되는 백 엔드 프로세스, hello WebJobs SDK는 새 메시지에 대 한 hello 큐를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="85c11-143">새 메시지가 나타나면 hello WebJob 해당 이미지에 대 한 미리 보기 만들고 해당 ad에 대 한 축소판 그림 URL 데이터베이스 필드를 hello 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="85c11-144">다음은 hello 부분 hello 응용 프로그램의 상호 작용 하는 방법을 보여 주는 다이어그램이입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Contoso Ads 아키텍처](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="85c11-146">hello 자습서 지침은.net 2.7.1 tooAzure SDK 적용 이상.</span><span class="sxs-lookup"><span data-stu-id="85c11-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="85c11-147"><a id="storage"></a>Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="85c11-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="85c11-148">Azure 저장소 계정을 hello 클라우드에서 큐 및 blob 데이터를 저장 하는 리소스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="85c11-149">또한 hello 대시보드에 대 한 hello WebJobs SDK toostore 로깅 데이터에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="85c11-150">실제 응용 프로그램에서는 일반적으로 응용 프로그램 데이터와 로깅 데이터를 위한 별도의 계정 및 테스트 데이터와 프로덕션 데이터를 위한 별도의 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="85c11-151">이 자습서에서는 하나의 계정만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="85c11-152">열기 hello **서버 탐색기** Visual Studio의 창.</span><span class="sxs-lookup"><span data-stu-id="85c11-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="85c11-153">마우스 오른쪽 단추로 클릭 hello **Azure** 노드를 차례로 클릭 한 다음 **tooMicrosoft Azure 구독 연결 중...** .</span><span class="sxs-lookup"><span data-stu-id="85c11-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![TooAzure 연결](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="85c11-155">Azure 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="85c11-156">마우스 오른쪽 단추로 클릭 **저장소** 아래에서 Azure 노드를 hello 및 클릭 **저장소 계정 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![저장소 계정 만들기](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="85c11-158">Hello에 **저장소 계정 만들기** 대화 상자에서 hello 저장소 계정의 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="85c11-159">hello 이름은 고유 해야 합니다 (다른 Azure 저장소 계정이 없으면 hello 점이 동일한 이름).</span><span class="sxs-lookup"><span data-stu-id="85c11-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="85c11-160">입력 한 hello 이름이 이미 사용 중이면 얻게 됩니다 기회 toochange 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="85c11-161">저장소 계정 수 URL tooaccess hello *{name}*. core.windows.net 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="85c11-162">집합 hello **지역 또는 선호도 그룹** 드롭 다운 목록 toohello 영역에 대 한 가장 가까운 tooyou 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="85c11-163">이 설정은 저장소 계정을 호스트할 Azure 데이터 센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="85c11-164">이 자습서의 경우 어떤 항목을 선택해도 두드러진 차이를 느낄 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="85c11-165">그러나 프로덕션 웹 앱에 대 한 원하는 웹 서버 및 사용자 저장소 계정 toobe hello에 동일한 지역 toominimize 대기 시간 및 데이터 요금을 송신 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="85c11-166">hello 웹 앱 (나중에 만들) 순서 toominimize 대기 시간에 hello 웹 앱에 액세스 가능한 toohello 브라우저 가까운 데이터 센터 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="85c11-167">집합 hello **복제** 드롭 다운 목록 너무**로컬 중복**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="85c11-168">저장소 계정에 대 한 지리적 복제를 사용 하는 경우 저장 된 hello 콘텐츠 hello 기본 위치에서 중요 재해가 발생 한 경우 복제 된 tooa 보조 데이터 센터 tooenable 장애 조치 toothat 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="85c11-169">지역에서 복제는 추가 비용을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="85c11-170">테스트 및 개발 계정에 대 한 일반적으로 원하지 toopay 지리적 복제에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="85c11-171">자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제](../storage/common/storage-create-storage-account.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="85c11-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="85c11-172">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-172">Click **Create**.</span></span>

    ![새 저장소 계정](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="85c11-174"><a id="download"></a>Hello 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="85c11-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="85c11-175">다운로드 하 고 hello 압축을 풀면 [솔루션 완료](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="85c11-176">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="85c11-177">Hello에서 **파일** 메뉴 선택 **열 > 프로젝트/솔루션**hello 솔루션을 다운로드 한 toowhere 이동한 다음 hello 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="85c11-178">CTRL + SHIFT + B toobuild hello 솔루션 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="85c11-179">기본적으로 Visual Studio 자동으로 복원 hello에 포함 되지 않은 hello NuGet 패키지 콘텐츠를 *.zip* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="85c11-180">Hello 패키지를 복원 하지 마십시오 하 여 수동으로 설치 거 toohello **솔루션에 대 한 NuGet 패키지 관리** hello를 클릭 하 고 대화 **복원** hello 상단 오른쪽에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="85c11-181">**솔루션 탐색기**, 다음 사항을 확인 **ContosoAdsWeb** hello 시작 프로젝트로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="85c11-182"><a id="configurestorage"></a>Hello 응용 프로그램 toouse 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="85c11-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="85c11-183">Hello 응용 프로그램을 열고 *Web.config* hello ContosoAdsWeb 프로젝트 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="85c11-184">SQL 연결 문자열 및 blob 및 큐 작업에 Azure 저장소 연결 문자열 hello 파일에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="85c11-185">SQL 연결 문자열 hello 가리키는 tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="85c11-186">hello 저장소 연결 문자열은 hello 저장소 계정 이름과 액세스 키에 대 한 자리 표시 자가 있는 예.</span><span class="sxs-lookup"><span data-stu-id="85c11-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="85c11-187">Hello 이름 및 사용자의 저장소 계정 키를 가진 연결 문자열과 함께이 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="85c11-188">저장소 연결 문자열 hello 라고 AzureWebJobsStorage hello 이름 hello WebJobs SDK를 사용 하기 때문에 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="85c11-189">hello hello Azure 환경에서에서 tooset 하나의 연결 문자열 값을 갖도록 동일한 이름이 여기 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="85c11-190">**서버 탐색기**, hello에서 저장소 계정에 마우스 오른쪽 단추로 클릭 **저장소** 노드를 차례로 클릭 한 다음 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![저장소 계정 속성 클릭](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="85c11-192">Hello에 **속성** 창 클릭 **저장소 계정 키**, 다음 hello 줄임표를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![저장소 계정 키](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="85c11-194">복사 hello **연결 문자열**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-194">Copy hello **Connection String**.</span></span>

    ![저장소 계정 키 대화 상자](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="85c11-196">Hello에 hello 저장소 연결 문자열을 바꾸기 *Web.config* 파일 방금 복사한 hello 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="85c11-197">붙여넣기 전에 hello 따옴표 점을 포함 하지 않고 hello 따옴표 안에 선택한 모든 항목이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="85c11-198">열기 hello *App.config* hello ContosoAdsWebJob 프로젝트 파일에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="85c11-199">이 파일에는 응용 프로그램 데이터를 위한 저장소 연결 문자열과 로깅을 위한 저장소 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="85c11-200">응용 프로그램 데이터와 로깅에 대한 별도의 저장소 계정을 사용할 수 있으며 [데이터에 대해 여러 저장소 계정](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="85c11-201">이 자습서에서는 단일 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="85c11-202">연결 문자열 hello hello 저장소 계정 키에 대 한 자리 표시자를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-202">hello connection strings have placeholders for hello storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="85c11-203">기본적으로 AzureWebJobsStorage 및 AzureWebJobsDashboard 라는 연결 문자열에 대 한 hello WebJobs SDK를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="85c11-204">수는 대신 [을 명시적으로 toohello에 전달 되지만 hello 연결 문자열을 저장 `JobHost` 개체](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="85c11-205">앞에서 복사한 hello 연결 문자열과 함께 두 저장소 연결 문자열을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="85c11-206">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-206">Save your changes.</span></span>

## <span data-ttu-id="85c11-207"><a id="run"></a>Hello 응용 프로그램을 로컬로 실행</span><span class="sxs-lookup"><span data-stu-id="85c11-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="85c11-208">toostart hello 웹 프런트 엔드 hello 응용 프로그램의 CTRL + f 5를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="85c11-209">hello 기본 브라우저 toohello 홈 페이지를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="85c11-210">(hello 웹 프로젝트를 변경한 후 때문에 실행 hello 시작 프로젝트입니다.)</span><span class="sxs-lookup"><span data-stu-id="85c11-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Contoso Ads 홈 페이지](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="85c11-212">hello 응용 프로그램의 toostart hello WebJob 백 엔드에 hello ContosoAdsWebJob 프로젝트를 마우스 오른쪽 단추로 클릭 **솔루션 탐색기**, 클릭 하 고 **디버그** > **새 인스턴스 시작** .</span><span class="sxs-lookup"><span data-stu-id="85c11-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="85c11-213">콘솔 응용 프로그램 창이 열리고 hello WebJobs SDK JobHost 개체 toorun 시작을 나타내는 로깅 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![해당 hello 백 엔드를 보여 주는 콘솔 응용 프로그램 창에서 실행 되](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="85c11-215">브라우저에서 **광고 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="85c11-216">테스트 데이터를 입력 하는 이미지 tooupload 선택한 다음 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![만들기 페이지](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="85c11-218">hello 앱 toohello 인덱스 페이지 까지일 처리 하는 아직 만들어지지 않은 때문에 새 ad hello에 대 한 미리 보기 표시 되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="85c11-219">한편, 잠시 후 hello 콘솔 응용 프로그램 창에 메시지를 로깅하는 보여 줍니다 큐 메시지 수신 및 처리 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![큐 메시지가 처리되었음을 나타내는 콘솔 응용 프로그램 창](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="85c11-221">Hello 콘솔 응용 프로그램 창에 메시지를 기록 하는 hello를 본 후 toosee hello 축소판 그림을 hello 인덱스 페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![인덱스 페이지](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="85c11-223">클릭 **세부 정보** ad toosee hello 큰 이미지에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![자세히 페이지](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="85c11-225">한 된를 실행 하면서 hello 응용 프로그램 로컬 컴퓨터에 하 하지만 사용자 컴퓨터에 있는 데이터베이스 큐와 작동 하 고 blob에 SQL Server를 사용 하는 클라우드 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="85c11-226">에서는 다음 단원을 hello 실행 hello 응용 프로그램 hello 클라우드에서 클라우드 데이터베이스 뿐만 아니라 클라우드 blob 및 큐를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="85c11-227"><a id="runincloud"></a>Hello 클라우드에서 hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="85c11-228">작업 단계 toorun hello 응용 프로그램 hello 클라우드에서 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="85c11-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="85c11-229">TooWeb 앱을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="85c11-230">Visual Studio는 앱 서비스의 새 웹앱 및 SQL 데이터베이스 인스턴스를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="85c11-231">웹 앱 toouse hello Azure SQL 데이터베이스 및 저장소 계정을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="85c11-232">Hello 클라우드에서 실행 하는 동안 일부 광고를 만든 후 WebJobs SDK 대시보드 toosee hello toooffer 기능 모니터링 풍부한 hello를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="85c11-233">TooWeb 앱 배포</span><span class="sxs-lookup"><span data-stu-id="85c11-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="85c11-234">Hello 브라우저 및 hello 콘솔 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="85c11-235">Hello에 hello 단계를 따라 [tooAzure SQL 데이터베이스와 게시](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) 섹션.</span><span class="sxs-lookup"><span data-stu-id="85c11-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="85c11-236">배포 하기 위한 hello 단계를 완료 한 후에이 문서의 hello 나머지 태스크를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="85c11-237">웹 앱 toouse hello Azure SQL 데이터베이스 및 저장소 계정 구성</span><span class="sxs-lookup"><span data-stu-id="85c11-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="85c11-238">보안 모범 사례를 너무 되었기[소스 코드 저장소에 저장 된 파일에서 연결 문자열과 같은 중요 한 정보를 넣지 마세요](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="85c11-239">Azure 제공 방법을 toodo 있는: hello Azure 환경에서에서 연결 문자열 및 기타 설정 값을 설정할 수 있습니다 및 ASP.NET 구성 Api 이러한 값을 Azure의 hello 응용 프로그램을 실행 하는 경우 자동으로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="85c11-240">사용 하 여 Azure에서 이러한 값을 설정할 수 **서버 탐색기**, Azure 포털, Windows PowerShell hello 또는 플랫폼 간 명령줄 인터페이스를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="85c11-241">자세한 내용은 [응용 프로그램 문자열 및 연결 문자열 작동 방식](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c11-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="85c11-242">이 섹션에서는 사용 **서버 탐색기** Azure에서 tooset 연결 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="85c11-243">**서버 탐색기**의 **Azure > App Service > {리소스 그룹}**에서 웹앱을 마우스 오른쪽 단추로 클릭한 다음 **설정 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="85c11-244">hello **Azure 웹 앱** hello에 창이 열립니다 **구성** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="85c11-245">Hello DefaultConnection 연결 문자열 toohello 이름의 hello 이름 변경 hello에 hello SQL 데이터베이스를 구성할 때 선택한 [tooAzure SQL 데이터베이스와 게시](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) 문서.</span><span class="sxs-lookup"><span data-stu-id="85c11-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="85c11-246">Azure는 hello 오른쪽 연결 문자열 값에 이미 있으므로 관련된 데이터베이스를 사용 하 여 hello 웹 응용 프로그램을 만든 경우이 연결 문자열을 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="85c11-247">코드를 찾고 hello 이름 toowhat 방금 변경 하려는 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="85c11-248">AzureWebJobsStorage 및 AzureWebJobsDashboard의 두 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="85c11-249">Hello 데이터베이스 유형을 너무 설정**사용자 지정**, 및 hello에 대 한 이전 사용한 동일한 값 집합 hello 연결 문자열 값 toohello *Web.config* 및 *App.config* 파일.</span><span class="sxs-lookup"><span data-stu-id="85c11-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="85c11-250">(있어야 hello 전체 연결 문자열 뿐 아니라 hello 액세스 키를 포함 하 고 hello 인용 부호를 포함 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="85c11-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="85c11-251">WebJobs SDK hello, 응용 프로그램 데이터에 대 한 및 로깅에 대 한 연결 문자열이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="85c11-252">앞에서 살펴본 것 처럼 응용 프로그램 데이터에 대 한 hello 하나도 hello 웹 프런트 엔드 코드에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="85c11-253">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-253">Click **Save**.</span></span>

    ![Azure 포털의 연결 문자열](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="85c11-255">**서버 탐색기**hello 웹 응용 프로그램을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **중지**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="85c11-256">Hello 웹 앱을 중지 한 후 hello 웹 응용 프로그램을 다시 마우스 오른쪽 단추로 클릭 하 고 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="85c11-257">hello WebJob을 게시 하지만 한 구성을 변경 하면 중지 하는 경우에 자동으로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="85c11-258">toorestart, hello 웹 앱을 다시 시작 하거나 hello에서 WebJob hello를 다시 시작 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="85c11-259">일반적으로 권장된 toorestart hello 웹 응용 프로그램의 구성 변경 후에 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="85c11-260">Hello 웹 앱 URL의 주소 표시줄에 있는 hello 브라우저 창을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="85c11-261">hello 홈 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-261">hello home page appears.</span></span>
8. <span data-ttu-id="85c11-262">때 수행한 것 처럼, 광고를 작성 하면 [hello 응용 프로그램을 로컬로 실행](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="85c11-263">hello 인덱스 페이지는 처음에 미리 보기 없이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="85c11-264">몇 초 후 hello 페이지를 새로 고치고 hello 축소판 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="85c11-265">Hello 축소판 그림 표시 되지 않으면 해야할 toowait는 1 분 정도 WebJob toorestart hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="85c11-266">잠시 후 작업 하는 경우 여전히 표시 되지 않으면 hello 축소판 그림 hello WebJob hello 페이지를 새로 고칠 때 자동으로 시작 되지 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="85c11-267">이 경우 toohello 이동 **응용 프로그램 서비스** hello 블레이드 [Azure 포털](https://portal.azure.com/)웹 앱을 찾은 다음 클릭 **시작**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="85c11-268">보기 hello WebJobs SDK 대시보드</span><span class="sxs-lookup"><span data-stu-id="85c11-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="85c11-269">Hello에 [Azure 포털](https://portal.azure.com/)선택, hello **응용 프로그램 서비스 블레이드**웹 앱을 찾아 선택 **WebJobs**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="85c11-270">선택 hello **로그** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-270">Select hello **Logs** tab.</span></span>

    ![로그 탭](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="85c11-272">새 브라우저 탭 toohello WebJobs SDK 대시보드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="85c11-273">hello 대시보드에 표시 해당 hello WebJob 실행 되 고 WebJobs SDK 트리거되는 hello 코드에서 함수 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="85c11-274">실행에 대 한 hello 함수 toosee 세부 사항 중 하나를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-274">Click one of hello functions toosee details about its execution.</span></span>

    ![WebJob SDK 대시보드](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJob SDK 대시보드](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="85c11-277">hello **재생 함수** 이 페이지에 단추 hello WebJobs SDK 프레임 워크 toocall hello 함수 다시 시키고 유효성 검사 하면 기회 toochange hello 전달 되는 데이터 toohello 함수 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="85c11-278">마치면 테스트는 것이 좋습니다 hello 웹 응용 프로그램, 저장소 계정 및 SQL 데이터베이스 인스턴스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="85c11-279">hello 웹 앱은 무료 이지만 hello SQL 저장소 계정 및 데이터베이스 인스턴스의 데이터베이스 비용이 (하지만 최소한의 toohello 작은 크기로 인해).</span><span class="sxs-lookup"><span data-stu-id="85c11-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="85c11-280">또한 hello 웹 응용 프로그램 실행을 종료 하는 경우 모든 사용자에 게 URL를 찾습니다 만들고 볼 수 광고 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="85c11-281">웹앱 삭제</span><span class="sxs-lookup"><span data-stu-id="85c11-281">Delete your web app</span></span>
<span data-ttu-id="85c11-282">Hello 포털에서 toohello 이동 **응용 프로그램 서비스** 블레이드를 웹 앱을 찾아서 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="85c11-283">Tootemporarily 방지 다른 원한다 면 hello 웹 앱에 액세스할 수 없게, 클릭 **중지** 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="85c11-284">이 경우 요금이 tooaccrue hello SQL 데이터베이스 및 저장소 계정에 대 한 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="85c11-285">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="85c11-285">Delete your storage account</span></span>
<span data-ttu-id="85c11-286">toodelete 저장소 계정의 참조 [저장소 계정을 삭제](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="85c11-287">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="85c11-287">Delete your database</span></span>
<span data-ttu-id="85c11-288">toodelete SQL hello 참조, 데이터베이스 [Azure SQL 데이터베이스 REST API](https://docs.microsoft.com/rest/api/sql/) 설명서입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="85c11-289"><a id="create"></a>처음부터 hello 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="85c11-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="85c11-290">작업이 섹션에서는 다음 작업 hello:</span><span class="sxs-lookup"><span data-stu-id="85c11-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="85c11-291">웹 프로젝트를 사용하여 Visual Studio 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="85c11-292">Hello 데이터에 대 한 클래스 라이브러리 프로젝트에 추가 hello 프런트 엔드 및 백 엔드 간에 공유 되는 액세스 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="85c11-293">WebJobs 배포가 사용 하도록 설정 된 hello 백 엔드에 대 한 콘솔 응용 프로그램 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="85c11-294">NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-294">Add NuGet packages.</span></span>
* <span data-ttu-id="85c11-295">프로젝트 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-295">Set project references.</span></span>
* <span data-ttu-id="85c11-296">Hello hello 자습서의 이전 섹션에서 사용한 hello 다운로드 한 응용 프로그램에서 응용 프로그램 코드 및 구성 파일을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="85c11-297">WebJobs SDK hello 및 Azure blob 및 큐로 사용 하는 hello 코드의 hello 부분을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="85c11-298">웹 프로젝트 및 클래스 라이브러리 프로젝트를 사용하여 Visual Studio 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="85c11-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="85c11-299">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="85c11-300">Hello에 **새 프로젝트** 대화 상자에서 선택 **Visual C#** > **웹** > **ASP.NET 웹 응용 프로그램 (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="85c11-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="85c11-301">Hello 프로젝트 ContosoAdsWeb hello 솔루션 ContosoAdsWebJobsSDK 이름을, (hello에 배치 하는 경우 hello 솔루션 이름을 변경 hello와 같은 폴더에 솔루션 다운로드)를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![새 프로젝트](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="85c11-303">Hello에 **새 ASP.NET 웹 응용 프로그램** 대화 상자에서 hello MVC 서식 파일을 선택 하 고 선택 **인증 변경**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![인증 변경](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="85c11-305">Hello에 **인증 변경** 대화 상자에서 선택 **인증 안 함**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![인증 없음](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="85c11-307">Hello에 **새 ASP.NET 웹 응용 프로그램** 대화 상자를 클릭 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="85c11-308">Visual Studio hello 솔루션과 hello 웹 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="85c11-309">**솔루션 탐색기**hello 솔루션 (하지: hello 프로젝트)를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="85c11-310">Hello에 **새 프로젝트 추가** 대화 상자에서 선택 **Visual C#** > **클래식 Windows 데스크톱** > **클래스 라이브러리 (.NET 프레임 워크)** 서식 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="85c11-311">이름 hello 프로젝트 *ContosoAdsCommon*, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="85c11-312">이 프로젝트는이 두 가지 프런트 엔드 hello hello Entity Framework 컨텍스트 및 hello 데이터 모델에 포함 됩니다 하 고 백 엔드 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="85c11-313">대신 hello 웹 프로젝트의 hello EF 관련 클래스를 정의 하 고 hello WebJob 프로젝트에서 해당 프로젝트를 참조할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="85c11-314">단, 다음 웹 작업 프로젝트는 필요 하지 않습니다는 참조 tooweb 어셈블리.</span><span class="sxs-lookup"><span data-stu-id="85c11-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="85c11-315">WebJob 배포가 설정된 콘솔 응용 프로그램 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="85c11-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="85c11-316">Hello 웹 프로젝트 (hello 솔루션이 아닌 또는 hello 클래스 라이브러리 프로젝트)를 마우스 오른쪽 단추로 누른 **추가** > **새 Azure WebJob 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project(새 Azure WebJob 프로젝트) 프로젝트 메뉴 선택 항목](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="85c11-318">Hello에 **Azure WebJob 추가** 대화 상자에서 두 hello로 ContosoAdsWebJob 입력 **프로젝트 이름** hello 및 **WebJob 이름은**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="85c11-319">둡니다 **WebJob 실행 모드** 도**지속적으로 실행**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="85c11-320">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-320">Click **OK**.</span></span>

   <span data-ttu-id="85c11-321">Visual Studio hello 웹 프로젝트를 배포할 때마다는 WebJob으로 구성 된 toodeploy는 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="85c11-322">즉, 수행 하는 것 hello 프로젝트를 만든 다음 작업을 수행 하는 hello toodo:</span><span class="sxs-lookup"><span data-stu-id="85c11-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="85c11-323">추가 *webjob 게시 settings.json* hello WebJob 프로젝트 속성 폴더의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="85c11-324">추가 *webjobs list.json* hello 웹 프로젝트 속성 폴더의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="85c11-325">Hello WebJob 프로젝트의 hello Microsoft.Web.WebJobs.Publish NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="85c11-326">이러한 변경에 대 한 자세한 내용은 참조 [어떻게 Visual Studio를 사용 하 여 WebJobs toodeploy](websites-dotnet-deploy-webjobs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="85c11-327">NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="85c11-327">Add NuGet packages</span></span>
<span data-ttu-id="85c11-328">웹 작업 프로젝트에 대 한 hello 새 프로젝트 템플릿은 hello WebJobs SDK NuGet 패키지를 자동으로 설치 [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) 와 그 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="85c11-329">Azure 저장소 클라이언트 라이브러리 (SCL) hello hello 웹 작업 프로젝트에 자동으로 설치 하는 WebJobs SDK 종속성은 hello 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="85c11-330">그러나 tooadd 해야 것 blob 및 큐로 toohello 웹 프로젝트 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="85c11-331">열기 hello **NuGet 패키지 관리** hello 솔루션에 대 한 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="85c11-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="85c11-332">Hello 왼쪽된 창에서 선택 **설치 된 패키지**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="85c11-333">Hello *Azure 저장소* 패키지를 선택한 다음 클릭 **관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="85c11-334">Hello에 **프로젝트 선택** 상자, 선택 hello **ContosoAdsWeb** 확인란을 선택한 다음 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="85c11-335">세 프로젝트 모두 Entity Framework toowork hello를 사용 하 여 SQL 데이터베이스의 데이터.</span><span class="sxs-lookup"><span data-stu-id="85c11-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="85c11-336">Hello 왼쪽된 창에서 선택 **온라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="85c11-337">Hello *EntityFramework* NuGet 패키지를 선택한 세 프로젝트 모두에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="85c11-338">프로젝트 참조 설정</span><span class="sxs-lookup"><span data-stu-id="85c11-338">Set project references</span></span>
<span data-ttu-id="85c11-339">참조 toohello ContosoAdsCommon 프로젝트가 모두 필요 하므로 hello SQL 데이터베이스, 웹 및 WebJob 프로젝트 모두 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="85c11-340">Hello ContosoAdsWeb 프로젝트 참조 toohello ContosoAdsCommon 프로젝트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="85c11-341">(Hello ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 누른 **추가** > **참조**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="85c11-342">Hello에 **참조 관리자** 대화 상자에서 **프로젝트** > **솔루션** > **ContosoAdsCommon**, 클릭 하 고 **확인**.)</span><span class="sxs-lookup"><span data-stu-id="85c11-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="85c11-343">hello WebJob 프로젝트 있어야 참조 이미지 작업에 대 한 연결 문자열에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="85c11-344">Hello ContosoAdsWebJob 프로젝트에 대 한 참조를 너무 설정`System.Drawing` 및 `System.Configuration`합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="85c11-345">코드 및 구성 파일 추가</span><span class="sxs-lookup"><span data-stu-id="85c11-345">Add code and configuration files</span></span>
<span data-ttu-id="85c11-346">이 자습서는 너무 어떻게 표시 되지 않습니다[MVC 컨트롤러와 뷰를 스 캐 폴딩을 사용 하 여 만들](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)어떻게 역시[SQL Server 데이터베이스를 사용 하는 Entity Framework 코드를 작성](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), 또는 [hello의 기본 사항 비동기 프로그래밍에 ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="85c11-347">따라서 모든 작업을 계속 toodo는 증가 hello 새 솔루션에 다운로드 한 hello 솔루션에서 코드 및 구성 파일 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="85c11-348">작업을 수행한 후 hello 다음 섹션에서는 표시 하 고 hello 코드의 주요 부분에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="85c11-349">tooadd 파일 tooa 프로젝트 또는 폴더, 마우스 오른쪽 단추로 클릭 hello 프로젝트 또는 폴더와 클릭 **추가** > **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="85c11-350">Select hello이 마우스 클릭 파일 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="85c11-351">기존 파일 tooreplace 사용할지 요청 되 면 클릭 **예**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="85c11-352">Hello ContosoAdsCommon 프로젝트에서 삭제 hello *Class1.cs* 파일을 다운로드 하는 hello 프로젝트에서 다음 파일이 해당 위치 hello에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="85c11-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="85c11-353">*Ad.cs*</span></span>
   * <span data-ttu-id="85c11-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="85c11-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="85c11-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="85c11-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="85c11-356">Hello ContosoAdsWeb 프로젝트 hello 파일 다운로드 hello 프로젝트에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="85c11-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="85c11-357">*Web.config*</span></span>
   * <span data-ttu-id="85c11-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="85c11-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="85c11-359">Hello에 *컨트롤러* 폴더: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="85c11-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="85c11-360">Hello에 *Views\Shared* 폴더: *_Layout.cshtml* 파일</span><span class="sxs-lookup"><span data-stu-id="85c11-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="85c11-361">Hello에 *Views\Home* 폴더: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="85c11-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="85c11-362">Hello에 *Views\Ad* 폴더 (먼저 hello 폴더 만들기): 5 *.cshtml* 파일</span><span class="sxs-lookup"><span data-stu-id="85c11-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="85c11-363">Hello ContosoAdsWebJob 프로젝트 hello 파일 다운로드 hello 프로젝트에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="85c11-364">*App.config* (hello 파일 형식 필터도 변경**모든 파일**)</span><span class="sxs-lookup"><span data-stu-id="85c11-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="85c11-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="85c11-365">*Program.cs*</span></span>
   * <span data-ttu-id="85c11-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="85c11-366">*Functions.cs*</span></span>

<span data-ttu-id="85c11-367">있습니다 수 이제 빌드, 실행 및 hello 자습서의 앞부분에서 설명 된 대로 hello 응용 프로그램을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="85c11-368">그러나 그렇게 하기 전에 hello hello 배포 하는 첫 번째 웹 앱에서 여전히 실행 되는 WebJob을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="85c11-369">그렇지 않으면, 해당 WebJob은 로컬로 만들어진 큐 메시지를 처리 하거나 hello 새 웹 앱에서 실행 중인 앱에서 사용 하는 모든 이후 hello 동일한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="85c11-370"><a id="code"></a>Hello 응용 프로그램 코드를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="85c11-371">hello 다음 섹션에서는 코드를 설명 hello tooworking hello WebJobs SDK로 및 Azure 저장소 blob 및 큐와 관련 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="85c11-372">Hello 코드 특정 toohello WebJobs SDK를 이동 toohello [Program.cs 및 Functions.cs](#programcs) 섹션.</span><span class="sxs-lookup"><span data-stu-id="85c11-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="85c11-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="85c11-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="85c11-374">hello Ad.cs 파일 ad 범주에 대 한 enum과 ad 정보에 대 한 POCO 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="85c11-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="85c11-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="85c11-376">hello ContosoAdsContext 클래스 hello Ad 클래스 Entity Framework는 SQL 데이터베이스에 저장 하는 DbSet 컬렉션에서 사용 되도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="85c11-377">hello 클래스에 두 명의 생성자입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-377">hello class has two constructors.</span></span> <span data-ttu-id="85c11-378">hello 먼저 hello 웹 프로젝트에 사용 되 고 hello Web.config 파일 또는 hello Azure 런타임 환경에 저장 된 연결 문자열의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="85c11-379">두 번째 생성자 hello toopass를 hello 실제 연결 문자열에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="85c11-380">만으로 hello WebJob 프로젝트 Web.config 파일을 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="85c11-381">했 듯이 여기서이 연결 문자열 저장 된 하 고 hello DbContext 클래스를 인스턴스화할 때 hello 코드 hello 연결 문자열을 검색 하는 어떻게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="85c11-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="85c11-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="85c11-383">hello `BlobInformation` 클래스는 큐 메시지에는 이미지 blob에 대 한 정보를 사용 하는 toostore 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="85c11-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="85c11-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="85c11-385">Hello에서 호출 되는 코드 `Application_Start` 메서드 만듭니다는 *이미지* blob 컨테이너 및 *이미지* 아직 없는 경우 큐에 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="85c11-386">이렇게 하면 새 저장소 계정 사용을 시작할 때마다 hello 필수를 blob 컨테이너 및 큐를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="85c11-387">코드 가져옵니다 액세스 toohello 저장소 계정에서 hello hello 저장소 연결 문자열을 사용 하 여 hello *Web.config* 파일 또는 Azure 런타임 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="85c11-388">그런 다음 참조 toohello 가져옵니다 *이미지* blob 컨테이너, 존재 하지 않는 액세스 hello 새 컨테이너에 대 한 권한을 설정 하는 경우 hello 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="85c11-389">기본적으로 새 컨테이너는 저장소 계정 자격 증명 tooaccess blob 사용한 클라이언트에만 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="85c11-390">hello 웹 앱 해당 지점 toohello 이미지 blob Url을 사용 하 여 이미지를 표시할 수 있도록 blob toobe 공개를 hello 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="85c11-391">비슷한 코드 참조 toohello 가져옵니다 *thumbnailrequest* 대기 및 새 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="85c11-392">이 경우에는 권한을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="85c11-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="85c11-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="85c11-394">hello *_Layout.cshtml* 파일 hello 머리글 및 바닥글에 hello 응용 프로그램 이름을 설정 하 고 "광고" 메뉴 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="85c11-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="85c11-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="85c11-396">hello *Views\Home\Index.cshtml* 파일 hello 홈 페이지에서 범주 링크를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="85c11-397">hello의 hello 정수 값을 전달 하는 hello 링크 `Category` 쿼리 문자열 변수 toohello 광고 인덱스 페이지에는 열거형입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="85c11-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="85c11-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="85c11-399">Hello에 *AdController.cs* 파일, hello 생성자 호출 hello `InitializeStorage` blob 및 큐를 사용 하기 위한 API를 제공 하는 메서드 toocreate Azure 저장소 클라이언트 라이브러리 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="85c11-400">그런 다음 hello 코드 가져옵니다 참조 toohello *이미지* 에서 이전에 본 것 처럼 컨테이너 blob *Global.asax.cs*합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="85c11-401">그 과정에서 웹앱에 해당하는 기본 [재시도 정책](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) (영문)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="85c11-402">hello 기본 지 수 백오프 재시도 정책을 일시적인 오류에 대 한 여러 번 시도에 1 분 보다 오랫동안 hello 웹 응용 프로그램 작동을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="85c11-403">여기에 지정 된 hello 재시도 정책을 toothree 시도를 각 시도 후 3 초 동안 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="85c11-404">비슷한 코드 참조 toohello 가져옵니다 *이미지* 큐입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="85c11-405">대부분의 hello 컨트롤러 코드는 DbContext 클래스를 사용 하 여 Entity Framework 데이터 모델을 사용 하기 위한 일반적인 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="85c11-406">예외는 hello HttpPost `Create` 메서드 파일을 업로드 하 고 blob 저장소에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="85c11-407">hello 모델 바인더를 제공는 [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello 메서드 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="85c11-408">Hello 사용자 파일 tooupload를 선택 하는 경우 hello 코드는 hello 파일을 업로드 하는 blob에 저장 및 toohello blob을 가리키는 URL로 hello Ad 데이터베이스 레코드를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="85c11-409">hello 코드 업로드 hello지 않습니다 하는 hello `UploadAndSaveBlobAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="85c11-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="85c11-410">Hello blob, 업로드 및 저장 hello 파일에 대 한 GUID 이름을 만들고 참조 toohello 저장 된 blob를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="85c11-411">Hello HttpPost 후 `Create` 메서드는 blob을 업로드 하 고 업데이트 hello 데이터베이스, 이미지는 변환 tooa 축소판 그림에 대 한 준비 큐 메시지 tooinform hello 백 엔드 프로세스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="85c11-412">HttpPost hello에 대 한 코드 hello `Edit` 메서드는 비슷하지만, hello 사용자가 새 이미지 파일을 선택 하는 경우이 ad에 이미 있는 모든 blob을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="85c11-413">광고를 삭제 하면 blob을 삭제 하는 hello 코드는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="85c11-414">ContosoAdsWeb - Views\Ad\Index.cshtml 및 Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="85c11-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="85c11-415">hello *Index.cshtml* 파일 축소판 그림 hello로 다른 ad 데이터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="85c11-416">hello *Details.cshtml* 파일 hello에 전체 이미지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="85c11-417">ContosoAdsWeb - Views\Ad\Create.cshtml 및 Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="85c11-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="85c11-418">hello *Create.cshtml* 및 *Edit.cshtml* 파일 인코딩을 hello 컨트롤러 tooget hello를 사용 하도록 설정 하는 폼은 지정 `HttpPostedFileBase` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="85c11-419">`<input>` 요소 파일 선택 대화 상자 hello 브라우저 tooprovide 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="85c11-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="85c11-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="85c11-421">때 hello WebJob가 시작 되 면 hello `Main` 메서드 호출 hello WebJobs SDK `JobHost.RunAndBlock` hello 현재 스레드에서 트리거된 함수의 메서드 toobegin 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="85c11-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail 메서드</span><span class="sxs-lookup"><span data-stu-id="85c11-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="85c11-423">WebJobs SDK hello 큐 메시지를 받을 때이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="85c11-424">hello 메서드 미리 보기를 만들고 넣습니다 hello 축소판 그림 hello 데이터베이스에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="85c11-425">hello `QueueTrigger` 특성 지시 hello WebJobs SDK toocall이이 메서드 hello thumbnailrequest 큐에서 새 메시지를 받으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="85c11-426">hello `BlobInformation` hello 큐 메시지의 개체는 자동으로 hello로 deserialize `blobInfo` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="85c11-427">Hello 메서드가 완료 되 면 hello 큐 메시지가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="85c11-428">완료 하기 전에 hello 메서드가 실패 하면 hello 큐 메시지 삭제 되지는 않습니다. 10 분 임대 만료 되 면 hello 메시지는 릴리스된 toobe 다시 선택 하 고 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="85c11-429">메시지가 항상 예외를 발생하는 경우에는 이 시퀀스가 무한 반복되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="85c11-430">Hello 메시지 이동된 tooa 큐 이름이 {queuename}는 5 실패 한 메시지 tooprocess 시도가-포이즌 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="85c11-431">hello 최대 시도 횟수는 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="85c11-432">두 개의 hello `Blob` 특성에 바인딩된 tooblobs 된 개체가 제공: 하나의 toohello 기존 이미지 blob 및 tooa 새 축소판 blob 하나 hello 메서드가 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="85c11-433">Blob 이름은 hello의 속성에서 가져온 `BlobInformation` hello 큐 메시지에서 받은 개체 (`BlobName` 및 `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="85c11-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="85c11-434">hello 저장소 클라이언트 라이브러리의 tooget hello의 전체 기능을 hello를 사용할 수 있습니다 `CloudBlockBlob` blob와 toowork 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="85c11-435">원하는 tooreuse 작성 된 코드의와 toowork `Stream` 개체 hello를 사용할 수 있습니다 `Stream` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="85c11-436">어떻게 toowrite 함수에 대 한 자세한 내용은 WebJobs SDK 특성을 사용 하 여 hello 다음 리소스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="85c11-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="85c11-437">Toouse Azure WebJobs SDK hello 사용 하 여 저장소를 대기 하는 방법</span><span class="sxs-lookup"><span data-stu-id="85c11-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="85c11-438">Toouse Azure blob 저장소 hello WebJobs SDK로 하는 방법</span><span class="sxs-lookup"><span data-stu-id="85c11-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="85c11-439">Toouse Azure 테이블 저장소 hello WebJobs SDK로 하는 방법</span><span class="sxs-lookup"><span data-stu-id="85c11-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="85c11-440">와 toouse Azure 서비스 버스 방법 hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="85c11-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="85c11-441">웹 앱에서는 여러 Vm에서 실행 하는 경우 여러 WebJobs 동시에 실행 되며 일부 시나리오에서 발생할 수 있습니다 hello 동일 데이터를 여러 번 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="85c11-442">기본 제공 hello 큐, blob 및 서비스 버스 트리거를 사용 하는 경우에 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="85c11-443">hello SDK 통해 각 메시지 또는 blob에 대 한 함수를 한 번만 처리할 수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="85c11-444">방법에 대 한 내용은 tooimplement 정상 종료 참조 [정상 종료](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="85c11-445">hello에 대 한 코드 hello `ConvertImageToThumbnailJPG` 메서드 (표시 되지 않음) 클래스를 사용 하 여 hello에 `System.Drawing` 편의상 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="85c11-446">그러나이 네임 스페이스의 hello 클래스는 Windows Forms 사용 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="85c11-447">Windows 또는 ASP.NET 서비스에서 사용할 수 있도록 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="85c11-448">이미지 처리 옵션에 대한 자세한 내용은 [동적 이미지 생성](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) 및 [이미지 크기 조정 세부 정보](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c11-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="85c11-449">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85c11-449">Next steps</span></span>
<span data-ttu-id="85c11-450">이 자습서에서는 백 엔드 처리를 위해 hello WebJobs SDK를 사용 하는 간단한 다중 계층 응용 프로그램에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="85c11-451">이 섹션에서는 ASP.NET 다중 계층 응용 프로그램 및 Webjob에 대해 더 알아볼 몇 가지 제안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="85c11-452">누락된 기능</span><span class="sxs-lookup"><span data-stu-id="85c11-452">Missing features</span></span>
<span data-ttu-id="85c11-453">hello 응용 프로그램은-시작 자습서에 대 한 간단한 유지 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="85c11-454">실제 응용 프로그램에서 구현 하는 [종속성 주입](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) hello 및 [리포지토리와의 단위 작업 패턴](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)를 사용 하 여 [로깅에 대 한 인터페이스](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), 사용[ EF Code First 마이그레이션을](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage 데이터 모델 변경이 및 사용 하 여 [EF 연결 복원 력](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage 일시적인 네트워크 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="85c11-455">WebJob 크기 조정</span><span class="sxs-lookup"><span data-stu-id="85c11-455">Scaling WebJobs</span></span>
<span data-ttu-id="85c11-456">WebJobs 웹 응용 프로그램의 hello 컨텍스트에서 실행 하며 개별적으로 확장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="85c11-457">예를 들어 표준 웹 앱 인스턴스 하나를 사용 하도록 설정한 경우 실행, 백그라운드 프로세스의 인스턴스가 하나만 있고 hello 서버 리소스 (CPU, 메모리 등) 그렇지 않은 경우 웹 콘텐츠를 사용할 수 있는 tooserve 수 중 일부를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="85c11-458">트래픽 요일 또는 요일의 시간에 따라 및 hello 백 엔드를 처리 해야 하는 경우 toodo 대기할 수 있는, 트래픽이 낮은 시간에 WebJobs toorun를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="85c11-459">해당 솔루션에 비해 너무 높거나 여전히 hello 부하 이면 목적으로 전용된 별도 웹 응용 프로그램에서 WebJob으로 hello 백 엔드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="85c11-460">그런 후 프런트 엔드 웹앱과는 별도로 백 엔드 웹앱을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="85c11-461">자세한 내용은 [WebJob 확장](websites-webjobs-resources.md#scale)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c11-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="85c11-462">웹앱 시간 제한 종료 방지</span><span class="sxs-lookup"><span data-stu-id="85c11-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="85c11-463">toomake 있는지 WebJobs 항상 실행 되 고 웹 응용 프로그램의 모든 인스턴스를 실행 해야 tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="85c11-464">Hello WebJobs 외부에서 WebJobs SDK를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="85c11-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="85c11-465">Hello WebJobs SDK를 사용 하는 프로그램에서 Azure 웹 작업에서 toorun이 되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="85c11-466">로컬에서 실행할 수 있고 클라우드 서비스 작업자 역할 또는 Windows 서비스와 같은 다른 환경에서도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="85c11-467">그러나 Azure 웹 앱을 통해 hello WebJobs SDK 대시보드에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="85c11-468">저장소 계정이 있습니다 tooconnect hello 웹 응용 프로그램 toohello hello에 hello AzureWebJobsDashboard 연결 문자열을 설정 하 여 사용 중인 toouse hello 대시보드 **구성** hello 클래식 포털을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="85c11-469">그런 다음 url hello를 사용 하 여 toohello 대시보드를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="85c11-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="85c11-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="85c11-471">자세한 내용은 참조 [hello WebJobs SDK로 로컬 개발에 대 한 대시보드를 가져오는](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), 있지만 이전 연결 문자열 이름을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c11-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="85c11-472">더 자세한 WebJob 설명서</span><span class="sxs-lookup"><span data-stu-id="85c11-472">More WebJobs documentation</span></span>
<span data-ttu-id="85c11-473">자세한 내용은 [Azure WebJob 설명서 리소스](http://go.microsoft.com/fwlink/?LinkId=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85c11-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
