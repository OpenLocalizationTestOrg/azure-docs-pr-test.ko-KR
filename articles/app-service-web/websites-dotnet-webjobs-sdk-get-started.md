---
title: "Azure App Service에서 .NET WebJob 만들기 | Microsoft Docs"
description: "ASP.NET MVC 및 Azure를 사용하여 다중 계층 앱을 만듭니다. 프런트 엔드는 Azure App Service의 웹앱에서 실행되고 백 엔드는 WebJob으로 실행됩니다. 앱에서는 Entity Framework, SQL 데이터베이스 및 Azure 저장소 큐와 Blob을 사용합니다."
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
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="41501-105">Azure 앱 서비스에서 .NET WebJob 만들기</span><span class="sxs-lookup"><span data-stu-id="41501-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="41501-106">이 자습서에서는 [WebJob SDK](websites-dotnet-webjobs-sdk.md)를 사용하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 코드를 작성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="41501-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="41501-107">[WebJobs SDK](websites-webjobs-resources.md) 목적은 WebJob이 이미지 처리, 큐 처리, RSS 집계, 파일 유지 관리, 전자 메일 보내기 등을 수행하는 일반적인 작업에 대해 작성하는 코드를 간소화하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="41501-108">WebJobs SDK에는 Azure 저장소 및 서비스 버스 작업, 작업 예약 및 오류 처리, 기타 여러 일반적인 시나리오를 위한 기본 제공 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="41501-109">또한 확장이 가능하기 때문에 [확장을 위한 오픈 소스 리포지토리](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview)도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="41501-110">샘플 응용 프로그램은 광고 게시판입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="41501-111">사용자는 광고에 대한 이미지를 업로드하고 백 엔드 과정은 이미지를 축소판 그림에 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="41501-112">광고 목록 페이지는 축소판 그림을 보여주고 광고 세부 정보 페이지는 전체 크기 이미지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="41501-112">The ad list page shows the thumbnails, and the ad details page shows the full-size image.</span></span> <span data-ttu-id="41501-113">다음 스크린샷을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-113">Here's a screenshot:</span></span>

![광고 목록](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="41501-115">이 샘플 응용 프로그램은 [Azure 큐](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 및 [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)과 함께 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="41501-116">이 자습서에서는 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) 및 [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279)에 응용 프로그램을 배포하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="41501-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="41501-117"><a id="prerequisites"></a>필수 조건</span><span class="sxs-lookup"><span data-stu-id="41501-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="41501-118">이 자습서에서는 Visual Studio에서 [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) 프로젝트를 작업하는 방법도 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="41501-119">이 자습서는 원래 Visual Studio 2013용으로 작성되었지만 이후 버전의 Visual Studio에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-119">The tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="41501-120">Visual Studio 2015 또는 2017을 사용하는 경우 응용 프로그램을 로컬로 실행하기 전에 Web.config 및 App.config에서 SQL Server LocalDB 연결 문자열의 `Data Source` 부분을 `Data Source=(localdb)\v11.0`에서 `Data Source=(LocalDb)\MSSQLLocalDB`로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-120">If you are using Visual Studio 2015 or 2017, make note that before you run the application locally, you must change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="41501-121"><a name="note"></a>이 자습서를 완료하려면 Azure 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-121"><a name="note"></a>You must have an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="41501-122">[Azure 계정을 무료로 개설](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)할 수 있음: 유료 Azure 서비스를 사용해볼 수 있는 크레딧을 받게 되며 크레딧을 모두 사용한 후에도 계정을 유지하고 무료 Azure 서비스(예: 웹 서비스)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use to try out paid Azure services, and even after they're used up, you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="41501-123">설정을 명시적으로 변경하여 결제를 요청하지 않는 한 신용 카드로 결제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-123">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="41501-124">[Visual Studio 구독자에 대한 월별 Azure 크레딧을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있음: Visual Studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="41501-125">Azure 계정을 등록하기 전에 Azure App Service를 시작하려면 [App Service 체험](https://azure.microsoft.com/try/app-service/)으로 이동합니다. 여기서 App Service의 단기 시작 웹앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-125">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="41501-126">신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="41501-127"><a id="learn"></a>학습할 내용</span><span class="sxs-lookup"><span data-stu-id="41501-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="41501-128">이 자습서에서는 다음 작업의 수행 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="41501-128">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="41501-129">Azure SDK를 설치하여 사용자 컴퓨터에서 Azure를 개발할 수 있도록 지원(Visual Studio 2013 및 2015 사용자에만 해당)</span><span class="sxs-lookup"><span data-stu-id="41501-129">Enable your machine for Azure development by installing the Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="41501-130">연결된 웹 프로젝트를 배포할 때 Azure WebJob으로 자동 배포되는 콘솔 응용 프로그램 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="41501-131">개발 컴퓨터에서 로컬로 WebJob SDK 백 엔드를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-131">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="41501-132">앱 서비스에서 웹앱에 있는 WebJob 백엔드로 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-132">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="41501-133">파일을 업로드하고 Azure Blob 서비스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-133">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="41501-134">Azure WebJob SDK를 사용하여 Azure 저장소 큐 및 Blob로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-134">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="41501-135"><a id="contosoads"></a>응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="41501-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="41501-136">이 샘플 응용 프로그램에서는 [큐 중심 작업 패턴](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 을 사용하여 미리 보기를 만드는 CPU 사용량이 많은 작업을 백 엔드 프로세스에 오프로드합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-136">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="41501-137">앱은 Entity Framework Code First를 사용해 SQL 데이터베이스에 광고를 저장하여 테이블을 만들고 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-137">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="41501-138">광고별로 데이터베이스는 전체 크기 이미지용과 미리 보기용으로 두 개의 URL을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-138">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![광고 테이블](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="41501-140">사용자가 이미지를 업로드하면 웹앱이 [Azure Blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)에 이미지를 저장하며 Blob을 가리키는 URL을 사용하여 데이터베이스에 광고 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-140">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="41501-141">이와 동시에 Azure 큐에 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-141">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="41501-142">Azure WebJob으로 실행되는 백 엔드 프로세스에서 WebJob SDK는 큐에서 새 메시지를 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-142">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="41501-143">새 메시지가 나타나면 WebJob은 해당 이미지의 미리 보기를 만들고 광고에 대한 미리 보기 URL 데이터베이스 필드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-143">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="41501-144">다음은 응용 프로그램의 여러 부분이 상호 작용하는 방법을 보여 주는 다이어그램입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-144">Here's a diagram that shows how the parts of the application interact:</span></span>

![Contoso Ads 아키텍처](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="41501-146">자습서 지침은 2.7.1.NET 이후에 Azure SDK를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-146">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="41501-147"><a id="storage"></a>Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="41501-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="41501-148">Azure 저장소 계정은 큐 및 Blob 데이터를 클라우드에 저장하기 위한 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-148">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="41501-149">WebJob SDK에서 대시보드에 대한 로깅 데이터를 저장하기 위해서도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-149">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="41501-150">실제 응용 프로그램에서는 일반적으로 응용 프로그램 데이터와 로깅 데이터를 위한 별도의 계정 및 테스트 데이터와 프로덕션 데이터를 위한 별도의 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="41501-151">이 자습서에서는 하나의 계정만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="41501-152">Visual Studio에서 **서버 탐색기** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41501-152">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="41501-153">**Azure** 노드를 마우스 오른쪽 단추로 클릭하고 **Microsoft Azure 구독에 연결...**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-153">Right-click the **Azure** node, and then click **Connect to Microsoft Azure Subscription...**.</span></span>
   
   ![Azure에 연결](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="41501-155">Azure 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="41501-156">Azure 노드 아래에서 **저장소**를 마우스 오른쪽 단추로 클릭하고 **저장소 계정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-156">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   
   ![저장소 계정 만들기](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="41501-158">**저장소 계정 만들기** 대화 상자에서 저장소 계정의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-158">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="41501-159">이 이름은 고유해야 합니다(다른 Azure 저장소 계정이 동일한 이름을 사용할 수 없음).</span><span class="sxs-lookup"><span data-stu-id="41501-159">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="41501-160">입력한 이름이 이미 사용 중이면 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-160">If the name you enter is already in use, you'll get a chance to change it.</span></span>

    <span data-ttu-id="41501-161">저장소 계정에 액세스하기 위한 URL은 *{name}*.core.windows.net입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-161">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="41501-162">**지역 또는 선호도 그룹** 드롭다운 목록을 가장 가까운 지역으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-162">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="41501-163">이 설정은 저장소 계정을 호스트할 Azure 데이터 센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="41501-164">이 자습서의 경우 어떤 항목을 선택해도 두드러진 차이를 느낄 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="41501-165">하지만 프로덕션 웹앱의 경우에는 대기 시간과 데이터 발신 요금을 최소화하기 위해 웹 서버와 저장소 계정을 동일한 지역에 두기 원할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-165">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="41501-166">나중에 만들게 될 웹앱은 대기 시간을 최소화하기 위해 웹앱에 액세스하는 브라우저에 가능한 한 가까워야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-166">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="41501-167">**복제** 드롭다운 목록을 **로컬 중복**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-167">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="41501-168">저장소 계정에 대해 지역에서 복제를 사용하는 경우에는 저장된 콘텐츠가 보조 위치에 복제되어 기본 위치에서 주요 재해가 발생하는 경우 보조 데이터 센터로 장애 조치(Failover)할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-168">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="41501-169">지역에서 복제는 추가 비용을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="41501-170">테스트 및 개발 계정의 경우 일반적으로 지역에서 복제 비용을 지불하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-170">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="41501-171">자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제](../storage/common/storage-create-storage-account.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="41501-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="41501-172">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-172">Click **Create**.</span></span>

    ![새 저장소 계정](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="41501-174"><a id="download"></a>응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="41501-174"><a id="download"></a>Download the application</span></span>
1. <span data-ttu-id="41501-175">[완료된 솔루션](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)을 다운로드하고 압축 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-175">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="41501-176">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="41501-177">**파일** 메뉴에서 **열기 > 프로젝트/솔루션**을 선택하고 솔루션을 다운로드한 위치로 이동한 후 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41501-177">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="41501-178">Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-178">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="41501-179">기본적으로 Visual Studio는 *.zip* 파일에 포함되지 않은 NuGet 패키지 콘텐츠를 자동으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-179">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="41501-180">패키지가 복원되지 않는 경우 **솔루션의 NuGet 패키지 관리** 대화 상자로 이동하고 오른쪽 위에서 **복원** 단추를 클릭하여 수동으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-180">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="41501-181">**솔루션 탐색기**에서 시작 프로젝트로 **ContosoAdsWeb**이 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <span data-ttu-id="41501-182"><a id="configurestorage"></a>저장소 계정을 사용하도록 응용 프로그램 구성</span><span class="sxs-lookup"><span data-stu-id="41501-182"><a id="configurestorage"></a>Configure the application to use your storage account</span></span>
1. <span data-ttu-id="41501-183">ContosoAdsWeb 프로젝트에서 응용 프로그램 *Web.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41501-183">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="41501-184">이 파일에는 Blob 및 큐 사용을 위한 SQL 연결 문자열과 Azure 저장소 연결 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-184">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="41501-185">SQL 연결 문자열은 [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) 데이터베이스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="41501-185">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="41501-186">저장소 연결 문자열은 저장소 계정 이름과 액세스 키에 대한 자리 표시자가 있는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-186">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="41501-187">이를 저장소 계정의 이름과 키가 포함된 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41501-187">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="41501-188">저장소 연결 문자열 이름은 WebJob SDK에서 기본적으로 사용하는 이름인 AzureWebJobsStorage입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-188">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="41501-189">Azure 환경에서 하나의 연결 문자열 값만 설정하면 되도록, 여기서는 같은 이름이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-189">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="41501-190">**서버 탐색기**에서 **저장소** 노드 아래에 있는 저장소 계정을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-190">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![저장소 계정 속성 클릭](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="41501-192">**속성** 창에서 **저장소 계정 키**를 클릭하고 줄임표를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-192">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![저장소 계정 키](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="41501-194">**연결 문자열**을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-194">Copy the **Connection String**.</span></span>

    ![저장소 계정 키 대화 상자](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="41501-196">*Web.config* 파일에서 저장소 연결 문자열을 방금 복사한 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41501-196">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="41501-197">붙여 넣기 전에 따옴표를 포함하지 않고 따옴표 안의 모든 내용을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-197">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="41501-198">ContosoAdsWebJob 프로젝트에서 *App.config* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41501-198">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="41501-199">이 파일에는 응용 프로그램 데이터를 위한 저장소 연결 문자열과 로깅을 위한 저장소 연결 문자열이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="41501-200">응용 프로그램 데이터와 로깅에 대한 별도의 저장소 계정을 사용할 수 있으며 [데이터에 대해 여러 저장소 계정](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs)을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="41501-201">이 자습서에서는 단일 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="41501-202">연결 문자열에는 저장소 계정 키의 자리 표시자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-202">The connection strings have placeholders for the storage account keys.</span></span>

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

    <span data-ttu-id="41501-203">기본적으로 WebJob SDK는 AzureWebJobsStorage 및 AzureWebJobsDashboard라는 연결 문자열을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-203">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="41501-204">또는 [원하는 연결 문자열을 저장한 후 `JobHost` 개체에 명시적으로 전달할 수 있습니다](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="41501-204">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="41501-205">저장소 연결 문자열을 둘 다 앞에서 복사한 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41501-205">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="41501-206">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-206">Save your changes.</span></span>

## <span data-ttu-id="41501-207"><a id="run"></a>로컬에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="41501-207"><a id="run"></a>Run the application locally</span></span>
1. <span data-ttu-id="41501-208">응용 프로그램의 웹 프런트 엔드를 시작하려면 Ctrl+F5를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="41501-208">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="41501-209">기본 브라우저는 홈 페이지로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="41501-209">The default browser opens to the home page.</span></span> <span data-ttu-id="41501-210">(웹 프로젝트를 시작 프로젝트로 만들었으므로 자동으로 실행됩니다.)</span><span class="sxs-lookup"><span data-stu-id="41501-210">(The web project runs because you've made it the startup project.)</span></span>

    ![Contoso Ads 홈 페이지](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="41501-212">응용 프로그램의 WebJob 백 엔드를 시작하려면 **솔루션 탐색기**에서 ContosoAdsWebJob 프로젝트를 마우스 오른쪽 단추로 클릭하고 **디버그** > **새 인스턴스 시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-212">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="41501-213">콘솔 응용 프로그램 창이 열리고 WebJob SDK JobHost 개체의 실행이 시작되었음을 나타내는 로깅 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-213">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![백 엔드가 실행 중임을 나타내는 콘솔 응용 프로그램 창](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="41501-215">브라우저에서 **광고 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="41501-216">일부 테스트 데이터를 입력하고 업로드할 이미지를 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-216">Enter some test data, select an image to upload, and then click **Create**.</span></span>

    ![만들기 페이지](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="41501-218">앱이 인덱스 페이지로 이동하지만 아직 처리가 이루어지지 않았기 때문에 새 광고에 대한 미리 보기를 표시하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-218">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="41501-219">잠시 후에 콘솔 응용 프로그램 창의 로깅 메시지에 큐 메시지가 수신되고 처리되었다는 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-219">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![큐 메시지가 처리되었음을 나타내는 콘솔 응용 프로그램 창](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="41501-221">콘솔 응용 프로그램 창에 로깅 메시지가 표시되면 인덱스 페이지를 새로 고쳐 미리 보기를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-221">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![인덱스 페이지](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="41501-223">광고에 해당하는 **자세히** 를 클릭하여 전체 크기 이미지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-223">Click **Details** for your ad to see the full-size image.</span></span>

    ![자세히 페이지](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="41501-225">로컬 컴퓨터에서 응용 프로그램을 실행하고 있으며, 해당 응용 프로그램은 컴퓨터에 있는 SQL Server 데이터베이스를 사용하고 있지만 클라우드의 큐 및 Blob을 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-225">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="41501-226">다음 섹션에서는 클라우드 데이터베이스와 클라우드 Blob 및 큐를 사용하여 클라우드에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-226">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="41501-227"><a id="runincloud"></a>클라우드에서 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="41501-227"><a id="runincloud"></a>Run the application in the cloud</span></span>
<span data-ttu-id="41501-228">클라우드에서 응용 프로그램을 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-228">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="41501-229">웹앱에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-229">Deploy to Web Apps.</span></span> <span data-ttu-id="41501-230">Visual Studio는 앱 서비스의 새 웹앱 및 SQL 데이터베이스 인스턴스를 자동으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="41501-231">Azure SQL 데이터베이스 및 저장소 계정을 사용하도록 웹앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-231">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="41501-232">클라우드에서 실행되는 동안 일부 광고를 만든 후에는 WebJob SDK 대시보드를 확인하면서 이 대시보드가 제공해야 하는 풍부한 모니터링 기능을 확인할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-232">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="41501-233">웹앱에 배포</span><span class="sxs-lookup"><span data-stu-id="41501-233">Deploy to Web Apps</span></span>

1. <span data-ttu-id="41501-234">브라우저 및 콘솔 응용 프로그램 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-234">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="41501-235">[SQL Database를 사용하여 Azure에 게시](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) 섹션의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="41501-235">Follow the steps in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="41501-236">배포 단계를 완료한 후 이 문서의 나머지 작업을 계속 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-236">After you complete the steps for deploying, continue with the remaining tasks in this article.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="41501-237">Azure SQL Database 및 저장소 계정을 사용하도록 웹앱 구성</span><span class="sxs-lookup"><span data-stu-id="41501-237">Configure the web app to use your Azure SQL database and storage account</span></span>
<span data-ttu-id="41501-238">[연결 문자열과 같은 민감한 정보를 소스 코드 리포지토리에 저장된 파일에 두지 않는 방식](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)(영문)이 보안 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-238">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="41501-239">Azure에서 이 작업을 수행할 수 있습니다. 즉, Azure 환경에서 연결 문자열 및 기타 설정 값을 지정하면 앱이 Azure에서 실행될 때 ASP.NET 구성 API가 해당 값을 자동으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-239">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="41501-240">**서버 탐색기**, Azure Portal, Windows PowerShell 또는 플랫폼 간 명령줄 인터페이스를 사용하여 Azure에서 이러한 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-240">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="41501-241">자세한 내용은 [응용 프로그램 문자열 및 연결 문자열 작동 방식](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="41501-242">이 섹션에서는 **서버 탐색기** 를 사용하여 Azure에서 연결 문자열 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-242">In this section, you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="41501-243">**서버 탐색기**의 **Azure > App Service > {리소스 그룹}**에서 웹앱을 마우스 오른쪽 단추로 클릭한 다음 **설정 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="41501-244">**Azure 웹앱** 창이 **구성** 탭에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="41501-244">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="41501-245">DefaultConnection 연결 문자열의 이름을 [SQL Database를 사용하여 Azure에 게시](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) 문서에서 SQL Database를 구성할 때 선택한 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-245">Change the name of the DefaultConnection connection string to the name you chose when you configured the SQL database in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="41501-246">Azure는 연결된 데이터베이스로 이 웹앱을 만들 때 이 연결 문자열을 자동으로 만들기 때문에 이미 적절한 연결 문자열 값이 지정되어 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-246">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="41501-247">코드가 찾는 이름으로 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-247">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="41501-248">AzureWebJobsStorage 및 AzureWebJobsDashboard의 두 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="41501-249">데이터베이스 유형을 **사용자 지정**으로 설정하고 연결 문자열 값을 이전에 *Web.config* 및 *App.config* 파일에 사용했던 것과 동일한 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-249">Set the database type to **Custom**, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="41501-250">액세스 키만이 아니라 전체 연결 문자열을 포함해야 하며 따옴표는 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-250">(Be sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="41501-251">이러한 연결 문자열은 WebJob SDK에서 응용 프로그램 데이터와 로깅에 각각 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-251">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="41501-252">앞서 살펴본 것처럼 응용 프로그램 데이터용 연결 문자열은 웹 프런트 엔드 코드에도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-252">As you saw earlier, the one for application data is also used by the web front-end code.</span></span>
4. <span data-ttu-id="41501-253">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-253">Click **Save**.</span></span>

    ![Azure 포털의 연결 문자열](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="41501-255">**서버 탐색기**에서 웹앱을 마우스 오른쪽 단추로 클릭하고 **중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-255">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="41501-256">웹앱이 중지된 후 웹앱을 마우스 오른쪽 단추로 다시 클릭하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-256">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="41501-257">WebJob은 게시될 때 자동으로 시작되지만 구성을 변경하면 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-257">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="41501-258">WebJob을 다시 시작하려면 [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715)에서 웹앱을 다시 시작하거나 WebJob을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-258">To restart it, you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="41501-259">일반적으로는 구성을 변경한 후에는 웹앱을 다시 시작하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-259">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="41501-260">주소 표시줄에 웹앱 URL이 표시되는 브라우저 창을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-260">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="41501-261">홈 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="41501-261">The home page appears.</span></span>
8. <span data-ttu-id="41501-262">[응용 프로그램을 로컬로 실행](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally)했을 때처럼 광고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-262">Create an ad, as you did when you [ran the application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="41501-263">처음에 미리 보기 없이 인덱스 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-263">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="41501-264">몇 초 후에 페이지를 새로 고치면 미리 보기가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="41501-264">Refresh the page after a few seconds and the thumbnail appears.</span></span>

   <span data-ttu-id="41501-265">축소판 그림이 표시되지 않으면 WebJob을 다시 시작하기 위해 일 분 정도 대기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-265">If the thumbnail doesn't appear, you might have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="41501-266">잠시 후에도 페이지를 새로 고칠 때 축소판 그림이 여전히 표시되지 않으면 WebJob은 자동으로 시작되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-266">If after a while, you still don't see the thumbnail when you refresh the page, the WebJob might not have started automatically.</span></span> <span data-ttu-id="41501-267">이 경우 [Azure Portal](https://portal.azure.com/)의 **App Services** 블레이드로 이동하여 웹앱을 찾은 다음 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-267">In that case, go to the **App Services** blade in the [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="41501-268">WebJob SDK 대시보드 보기</span><span class="sxs-lookup"><span data-stu-id="41501-268">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="41501-269">[Azure Portal](https://portal.azure.com/)에서 **App Services 블레이드**를 선택하고 웹앱을 찾은 후 **WebJobs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-269">In the [Azure portal](https://portal.azure.com/), select the **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="41501-270">**로그** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-270">Select the **Logs** tab.</span></span>

    ![로그 탭](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="41501-272">새 브라우저 탭에서 WebJob SDK 대시보드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="41501-272">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="41501-273">이 대시보드에는 WebJob이 실행 중이라고 표시되며 WebJob SDK가 트리거한 코드의 함수 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-273">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="41501-274">함수 중 하나를 클릭하여 실행에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-274">Click one of the functions to see details about its execution.</span></span>

    ![WebJob SDK 대시보드](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJob SDK 대시보드](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="41501-277">이 페이지의 **Replay Function(함수 재생)** 단추를 클릭하면 WebJob SDK 프레임워크가 해당 함수를 다시 호출하며 처음에 함수에 전달된 데이터를 변경할 기회가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-277">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="41501-278">테스트를 마치면 웹앱, 저장소 계정 및 SQL Database 인스턴스를 삭제하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-278">When you're finished testing, consider deleting the web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="41501-279">웹앱은 무료이지만 SQL 저장소 계정 및 데이터베이스 인스턴스는 요금이 부과됩니다(크기가 작으므로 소량 부과됨).</span><span class="sxs-lookup"><span data-stu-id="41501-279">The web app is free, but the SQL storage account and database instance accrue charges (albeit, minimal due to the small size).</span></span> <span data-ttu-id="41501-280">또한 이 앱을 실행 중인 채로 두는 경우에는 누군가가 URL을 발견하면 광고를 만들고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-280">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="41501-281">웹앱 삭제</span><span class="sxs-lookup"><span data-stu-id="41501-281">Delete your web app</span></span>
<span data-ttu-id="41501-282">포털에서 **App Services** 블레이드로 이동하여 웹앱을 찾아서 선택하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-282">In the portal, go to the **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="41501-283">임시로 다른 사람이 웹 앱에 액세스하지 못하도록 하려면 대신 **중지** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-283">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="41501-284">이 경우에는 SQL 데이터베이스 및 저장소 계정에 대해 요금이 계속해서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-284">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="41501-285">저장소 계정 삭제</span><span class="sxs-lookup"><span data-stu-id="41501-285">Delete your storage account</span></span>
<span data-ttu-id="41501-286">저장소 계정을 삭제하려면 [저장소 계정 삭제](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-286">To delete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="41501-287">데이터베이스 삭제</span><span class="sxs-lookup"><span data-stu-id="41501-287">Delete your database</span></span>
<span data-ttu-id="41501-288">SQL Database를 삭제하려면 [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-288">To delete your SQL database, see the [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="41501-289"><a id="create"></a>처음부터 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="41501-289"><a id="create"></a>Create the application from scratch</span></span>
<span data-ttu-id="41501-290">이 섹션에서는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-290">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="41501-291">웹 프로젝트를 사용하여 Visual Studio 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="41501-292">프런트 엔드와 백 엔드 간에 공유되는 데이터 액세스 계층에 대한 클래스 라이브러리 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-292">Add a class library project for the data access layer that is shared between the front end and back end.</span></span>
* <span data-ttu-id="41501-293">WebJob 배포를 설정한 상태로 백 엔드에 대한 콘솔 응용 프로그램 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-293">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="41501-294">NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-294">Add NuGet packages.</span></span>
* <span data-ttu-id="41501-295">프로젝트 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-295">Set project references.</span></span>
* <span data-ttu-id="41501-296">자습서 이전 섹션에서 사용했던 다운로드한 응용 프로그램의 응용 프로그램 코드 및 구성 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-296">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="41501-297">Azure Blob 및 큐와 WebJob SDK를 사용하는 코드 부분을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-297">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="41501-298">웹 프로젝트 및 클래스 라이브러리 프로젝트를 사용하여 Visual Studio 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="41501-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="41501-299">Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="41501-300">**새 프로젝트** 대화 상자에서 **Visual C#** > **웹** > **ASP.NET 웹 응용 프로그램(.NET Framework)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-300">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="41501-301">프로젝트 이름을 ContosoAdsWeb으로, 솔루션 이름을 ContosoAdsWebJobsSDK로 지정하고(다운로드한 솔루션과 같은 폴더에 배치하는 경우에는 솔루션 이름 변경) **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-301">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![새 프로젝트](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="41501-303">**새 ASP.NET 웹 응용 프로그램** 대화 상자에서 MVC 템플릿을 선택하고 **인증 변경**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-303">In the **New ASP.NET Web Application** dialog, choose the MVC template, and select **Change Authentication**.</span></span>

    ![인증 변경](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="41501-305">**인증 변경** 대화 상자에서 **인증 없음**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-305">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![인증 없음](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="41501-307">**새 ASP.NET 웹 응용 프로그램** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-307">In the **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="41501-308">Visual Studio에서 솔루션 및 웹 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-308">Visual Studio creates the solution and the web project.</span></span>
7. <span data-ttu-id="41501-309">**솔루션 탐색기**에서 솔루션(프로젝트 아님)을 마우스 오른쪽 단추로 클릭하고 **추가** > **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-309">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="41501-310">**새 프로젝트 추가** 대화 상자에서 **Visual C#** > **Windows 클래식 데스크톱** > **클래스 라이브러리(.NET Framework)** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-310">In the **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="41501-311">프로젝트의 이름을 *ContosoAdsCommon*으로 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-311">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="41501-312">이 프로젝트에는 프런트 엔드 및 백 엔드 둘 다에서 사용할 Entity Framework 컨텍스트와 데이터 모델이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-312">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="41501-313">또는 웹 프로젝트에서 EF 관련 클래스를 정의하고 WebJob 프로젝트에서 이 프로젝트를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-313">As an alternative, you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="41501-314">하지만 WebJob 프로젝트에는 필요 없는 웹 어셈블리 참조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-314">But, then your WebJob project would have a reference to web assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="41501-315">WebJob 배포가 설정된 콘솔 응용 프로그램 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="41501-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="41501-316">웹 프로젝트(솔루션 또는 클래스 라이브러리 프로젝트 아님)를 마우스 오른쪽 단추로 클릭하고 **추가** > **New Azure WebJob Project(새 Azure WebJob 프로젝트)**를 사용하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 코드를 작성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="41501-316">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![New Azure WebJob Project(새 Azure WebJob 프로젝트) 프로젝트 메뉴 선택 항목](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="41501-318">**Azure WebJob 추가** 대화 상자에서 **프로젝트 이름**과 **WebJob 이름**으로 ContosoAdsWebJob을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-318">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="41501-319">**WebJob 실행 모드**를 **계속 실행**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-319">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="41501-320">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-320">Click **OK**.</span></span>

   <span data-ttu-id="41501-321">Visual Studio는 웹 프로젝트를 배포할 때마다 WebJob으로 배포되도록 구성된 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-321">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="41501-322">이렇게 하기 위해 프로젝트를 만든 후에 다음 작업을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-322">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="41501-323">WebJob 프로젝트 속성 폴더에 *webjob-publish-settings.json* 파일을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-323">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="41501-324">웹 프로젝트 속성 폴더에 *webjobs-list.json* 파일을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-324">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="41501-325">WebJob 프로젝트에 Microsoft.Web.WebJobs.Publish NuGet 패키지를 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-325">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="41501-326">이러한 변경에 대한 자세한 내용은 [Visual Studio를 사용하여 WebJob을 배포하는 방법](websites-dotnet-deploy-webjobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-326">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="41501-327">NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="41501-327">Add NuGet packages</span></span>
<span data-ttu-id="41501-328">WebJob 프로젝트에 대한 new-project 템플릿이 WebJobs SDK NuGet 패키지 [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) 와 해당 종속성을 자동으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-328">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="41501-329">WebJob 프로젝트에서 자동으로 설치되는 WebJob SDK 종속성 중 하나는 Azure SCL(저장소 클라이언트 라이브러리)입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-329">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="41501-330">그러나 Blob 및 큐 작업을 수행하려면 웹 프로젝트에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-330">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="41501-331">솔루션에 대한 **NuGet 패키지 관리** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="41501-331">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="41501-332">왼쪽 창에서 **설치된 패키지**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-332">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="41501-333">*Azure Storage* 패키지를 찾은 후 **관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-333">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="41501-334">**프로젝트 선택** 상자에서 **ContosoAdsWeb** 확인란을 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-334">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="41501-335">이러한 세 프로젝트는 SQL 데이터베이스의 데이터를 사용하기 위해 Entity Framework를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-335">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="41501-336">왼쪽 창에서 **온라인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-336">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="41501-337">*EntityFramework* NuGet 패키지를 찾아 세 개의 프로젝트 모두에서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-337">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="41501-338">프로젝트 참조 설정</span><span class="sxs-lookup"><span data-stu-id="41501-338">Set project references</span></span>
<span data-ttu-id="41501-339">웹 및 WebJob 프로젝트 둘 다에서 SQL 데이터베이스를 사용하므로 ContosoAdsCommon 프로젝트에 대한 참조가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-339">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="41501-340">ContosoAdsWeb 프로젝트에서 ContosoAdsCommon 프로젝트에 대한 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-340">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="41501-341">ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **추가** > **참조**를 사용하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 코드를 작성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="41501-341">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="41501-342">**참조 관리자** 대화 상자에서 **프로젝트** > **솔루션** > **ContosoAdsCommon**을 차례로 선택한 후 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-342">In the **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="41501-343">WebJob 프로젝트는 이미지를 사용하고 연결 문자열에 액세스하기 위해 참조가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-343">The WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="41501-344">ContosoAdsWebJob 프로젝트에서 `System.Drawing` 및 `System.Configuration`에 대한 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-344">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="41501-345">코드 및 구성 파일 추가</span><span class="sxs-lookup"><span data-stu-id="41501-345">Add code and configuration files</span></span>
<span data-ttu-id="41501-346">이 자습서에 [스캐폴딩을 사용하여 MVC 컨트롤러 및 보기를 만드는 방법](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)(영문), [SQL Server 데이터베이스를 사용하는 Entity Framework 코드를 작성하는 방법](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)(영문) 또는 [ASP.NET 4.5의 비동기 프로그래밍에 대한 기본 사항](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async)(영문)은 나와 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-346">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="41501-347">이 작업을 수행하려면 다운로드한 솔루션에서 새 솔루션으로 코드 및 구성 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-347">So, all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="41501-348">이 작업을 수행한 후에는 다음 섹션에서 코드의 핵심 부분에 대한 설명을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-348">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="41501-349">프로젝트나 폴더에 파일을 추가하려면 프로젝트나 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **기존 항목**를 사용하는 간단한 다중 계층 ASP.NET MVC 5 응용 프로그램에 코드를 작성하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="41501-349">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="41501-350">원하는 파일을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-350">Select the files you want and click **Add**.</span></span> <span data-ttu-id="41501-351">기존 파일을 바꿀지 여부를 묻는 메시지가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-351">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="41501-352">ContosoAdsCommon 프로젝트에서 *Class1.cs* 파일을 삭제하고 그 자리에 다운로드한 프로젝트의 다음 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-352">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="41501-353">*Ad.cs*</span><span class="sxs-lookup"><span data-stu-id="41501-353">*Ad.cs*</span></span>
   * <span data-ttu-id="41501-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="41501-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="41501-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="41501-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="41501-356">ContosoAdsWeb 프로젝트에 다운로드한 프로젝트에서 가져온 다음 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-356">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="41501-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="41501-357">*Web.config*</span></span>
   * <span data-ttu-id="41501-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="41501-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="41501-359">*Controllers* 폴더: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="41501-359">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="41501-360">*Views\Shared* 폴더: *_Layout.cshtml* 파일</span><span class="sxs-lookup"><span data-stu-id="41501-360">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="41501-361">*Views\Home* 폴더: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="41501-361">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="41501-362">*Views\Ad* 폴더(먼저 폴더 만들기): 5개의 *.cshtml* 파일</span><span class="sxs-lookup"><span data-stu-id="41501-362">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="41501-363">ContosoAdsWebJob 프로젝트에서 다운로드한 프로젝트에서 가져온 다음 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-363">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="41501-364">*App.config* (파일 형식 필터를 **모든 파일**로 변경)</span><span class="sxs-lookup"><span data-stu-id="41501-364">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="41501-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="41501-365">*Program.cs*</span></span>
   * <span data-ttu-id="41501-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="41501-366">*Functions.cs*</span></span>

<span data-ttu-id="41501-367">이제 자습서의 앞부분에 설명된 대로 응용 프로그램을 빌드, 실행 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-367">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="41501-368">이 작업을 수행하기 전에 배포한 첫 번째 웹앱에서 여전히 실행되고 있는 WebJob을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-368">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="41501-369">그렇지 않으면 모두가 동일한 저장소 계정을 사용하고 있으므로 해당 WebJob이 로컬로 만들어졌거나 새 웹앱에서 실행되고 있는 앱에 의해 만들어진 큐 메시지를 처리하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-369">Otherwise, that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <span data-ttu-id="41501-370"><a id="code"></a>응용 프로그램 코드 검토</span><span class="sxs-lookup"><span data-stu-id="41501-370"><a id="code"></a>Review the application code</span></span>
<span data-ttu-id="41501-371">다음 섹션에서는 WebJob SDK 및 Azure 저장소 Blob와 큐 작업과 관련된 코드에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-371">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="41501-372">WebJob SDK 관련 코드의 경우 [Program.cs 및 Functions.cs](#programcs) 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-372">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="41501-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="41501-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="41501-374">Ad.cs 파일은 광고 범주의 열거형 및 광고 정보에 대한 POCO 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-374">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="41501-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="41501-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="41501-376">ContosoAdsContext 클래스는 DbSet 컬렉션에서 Ad 클래스가 사용된다는 것을 지정하며, Entity Framework는 이를 SQL 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-376">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="41501-377">이 클래스에는 두 개의 생성자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-377">The class has two constructors.</span></span> <span data-ttu-id="41501-378">첫 번째 생성자는 웹 프로젝트에서 사용되며 Web.config 파일 또는 Azure 런타임 환경에 저장되는 연결 문자열의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-378">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="41501-379">두 번째 생성자는 실제 연결 문자열을 전달할 수 있게 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-379">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="41501-380">이 과정은 WebJob 프로젝트에서 필요합니다. 여기에는 Web.config 파일이 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-380">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="41501-381">앞에서 이 연결 문자열이 저장된 위치를 확인했으며, 이후에 코드가 DbContext 클래스를 인스턴스화할 때 연결 문자열을 검색하는 방법을 확인하게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-381">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="41501-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="41501-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="41501-383">`BlobInformation` 클래스는 큐 메시지의 이미지 Blob에 대한 정보를 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-383">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

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


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="41501-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="41501-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="41501-385">`Application_Start` 메서드에서 호출되는 코드는 *images* Blob 컨테이너 및 *images* 큐를 만듭니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="41501-385">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="41501-386">따라서 새 저장소 계정을 사용하기 시작할 때마다 필수 Blob 컨테이너와 큐가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="41501-386">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="41501-387">이 코드는 *Web.config* 파일 또는 Azure 런타임 환경의 저장소 연결 문자열을 사용하여 저장소 계정에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-387">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="41501-388">그런 다음, *images* Blob 컨테이너에 대한 참조를 가져오고 컨테이너를 만들고(아직 없는 경우) 새 컨테이너에 대한 액세스 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-388">Then, it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="41501-389">기본적으로 새 컨테이너는 저장소 계정 자격 증명이 있는 클라이언트만 Blob에 액세스를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-389">By default, new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="41501-390">이미지 Blob을 가리키는 URL을 사용하여 이미지를 표시할 수 있도록 웹앱은 Blob을 공개로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-390">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="41501-391">비슷한 코드가 *thumbnailrequest* 큐에 대한 참조를 가져오고 새 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-391">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="41501-392">이 경우에는 권한을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="41501-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="41501-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="41501-394">*_Layout.cshtml* 파일은 머리글과 바닥글에서 앱 이름을 설정하고 "Ads" 메뉴 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-394">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="41501-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="41501-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="41501-396">*Views\Home\Index.cshtml* 파일은 홈페이지에 범주 링크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-396">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="41501-397">이 링크는 쿼리 문자열 변수의 `Category` 열거형 정수 값을 광고 인덱스 페이지에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-397">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="41501-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="41501-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="41501-399">*AdController.cs* 파일에서 생성자는 `InitializeStorage` 메서드를 호출하여 Blob 및 큐 작업을 위한 API를 제공하는 Azure Storage 클라이언트 라이브러리 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-399">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="41501-400">그런 다음 이 코드는 앞서 *Global.asax.cs*에서 확인한 *images* Blob 컨테이너에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="41501-400">Then, the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="41501-401">그 과정에서 웹앱에 해당하는 기본 [재시도 정책](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) (영문)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="41501-402">기본 지수 백오프 재시도 정책은 일시적 오류에 대해 반복적으로 재시도하는 경우 1분 넘게 웹앱을 중지시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-402">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="41501-403">여기에 지정된 재시도 정책은 각 시도 후 3초 동안 최대 3회까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-403">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="41501-404">비슷한 코드가 *images* 큐에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="41501-404">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="41501-405">대부분의 컨트롤러 코드는 DbContext 클래스를 사용한 Entity Framework 데이터 모델 작업에 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-405">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="41501-406">예외는 HttpPost `Create` 서드이며, 이 메서드는 파일을 업로드하고 Blob 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-406">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="41501-407">모델 바인더는 메서드에 [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-407">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="41501-408">사용자가 업로드할 파일을 선택한 경우 코드는 파일을 업로드하고 Blob에 저장하며 광고 데이터베이스 레코드를 Blob을 가리키는 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-408">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="41501-409">업로드를 수행하는 코드는 `UploadAndSaveBlobAsync` 메서드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-409">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="41501-410">Blob에 대한 GUID 이름을 만들고, 파일을 업로드 및 저장하며, 저장된 Blob에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-410">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="41501-411">HttpPost `Create` 메서드가 Blob을 업로드하고 데이터베이스를 업데이트한 후에는 이미지를 미리 보기로 변환할 수 있는 백 엔드 프로세스에 대해 알리는 큐 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="41501-411">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="41501-412">HttpPost `Edit` 메서드의 코드도 비슷하지만, 사용자가 새 이미지 파일을 선택하면 이 광고에 대해 이미 존재하는 Blob을 삭제해야 한다는 점은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="41501-412">The code for the HttpPost `Edit` method is similar, except that if the user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="41501-413">다음은 광고를 삭제하면 Blob를 삭제하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="41501-413">Here is the code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="41501-414">ContosoAdsWeb - Views\Ad\Index.cshtml 및 Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="41501-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="41501-415">*Index.cshtml* 파일은 다른 광고 데이터가 포함된 미리 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-415">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="41501-416">*Details.cshtml* 파일은 전체 크기 이미지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-416">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="41501-417">ContosoAdsWeb - Views\Ad\Create.cshtml 및 Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="41501-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="41501-418">*Create.cshtml* 및 *Edit.cshtml* 파일은 컨트롤러가 `HttpPostedFileBase` 개체를 가져올 수 있게 하는 양식 인코딩을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-418">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="41501-419">`<input>` 요소는 파일 선택 대화 상자를 제공하도록 브라우저에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-419">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="41501-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="41501-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="41501-421">WebJob이 시작되면 `Main` 메서드가 WebJob SDK `JobHost.RunAndBlock` 메서드를 호출하여 현재 스레드에서 트리거한 함수의 실행을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-421">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="41501-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail 메서드</span><span class="sxs-lookup"><span data-stu-id="41501-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="41501-423">WebJob SDK는 큐 메시지가 수신될 때 이 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-423">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="41501-424">이 메서드는 미리 보기를 만든 후 데이터베이스에 미리 보기 URL을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-424">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

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
            // be instantiated and disposed within the function.
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

* <span data-ttu-id="41501-425">`QueueTrigger` 특성은 thumbnailrequest 큐에 새 메시지가 수신될 때 WebJob SDK가 이 메서드를 호출하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-425">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="41501-426">큐 메시지의 `BlobInformation` 개체는 자동으로 `blobInfo` 매개 변수로 역직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-426">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="41501-427">이 메서드가 완료되면 큐 메시지가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-427">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="41501-428">완료되기 전에 메서드가 실패하면 큐 메시지는 삭제되지 않고 10분의 임대 기간이 만료되면 선택하여 처리할 수 있게 메시지가 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-428">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="41501-429">메시지가 항상 예외를 발생하는 경우에는 이 시퀀스가 무한 반복되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="41501-430">메시지 처리 시도가 5회 연속으로 실패하면 메시지는 {queuename}-poison 큐로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-430">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="41501-431">최대 시도 횟수는 구성 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-431">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="41501-432">두 `Blob` 특성은 Blob에 바인딩된 개체를 제공합니다. 하나는 기존 이미지 Blob에 바인딩되고 다른 하나는 메서드가 만드는 새 축소판 그림 Blob에 바인딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-432">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="41501-433">Blob 이름은 큐 메시지(`BlobName` 및 `BlobNameWithoutExtension`)에 수신된 `BlobInformation` 개체의 속성을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-433">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="41501-434">저장소 클라이언트 라이브러리의 전기능을 사용하려는 경우 `CloudBlockBlob` 클래스를 사용하여 Blob을 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-434">To get the full functionality of the Storage Client Library, you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="41501-435">`Stream` 개체 사용을 위해 작성한 코드를 다시 사용하려면 `Stream` 클래스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-435">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="41501-436">WebJobs SDK 특성을 사용하는 함수를 작성하는 방법에 대한 자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-436">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="41501-437">WebJobs SDK를 사용하여 Azure 큐 저장소로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="41501-437">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="41501-438">WebJob SDK를 사용하여 Azure Blob 저장소로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="41501-438">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="41501-439">WebJob SDK를 사용하여 Azure 테이블 저장소로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="41501-439">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="41501-440">WebJob SDK를 사용하여 Azure 서비스 버스로 작업하는 방법</span><span class="sxs-lookup"><span data-stu-id="41501-440">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="41501-441">웹앱이 여러 VM에서 실행되는 경우 여러 WebJob이 동시에 실행되며, 일부 시나리오에서 이렇게 하면 동일한 데이터를 여러 번 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="41501-442">기본 제공 큐, blob 및 서비스 버스 트리거를 사용하는 경우 이는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-442">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="41501-443">SDK는 각 메시지 또는 blob에 대해 함수를 한 번만 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-443">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="41501-444">정상 종료를 구현하는 방법에 대한 자세한 내용은 [정상 종료](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-444">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="41501-445">`ConvertImageToThumbnailJPG` 메서드의 코드(표시되지 않음)는 간소화를 위해 `System.Drawing` 네임스페이스의 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-445">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="41501-446">하지만 이 네임스페이스의 클래스는 Windows Forms에서 사용하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-446">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="41501-447">Windows 또는 ASP.NET 서비스에서 사용할 수 있도록 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="41501-448">이미지 처리 옵션에 대한 자세한 내용은 [동적 이미지 생성](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) 및 [이미지 크기 조정 세부 정보](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="41501-449">다음 단계</span><span class="sxs-lookup"><span data-stu-id="41501-449">Next steps</span></span>
<span data-ttu-id="41501-450">이 자습서에서는 백 엔드 처리를 위해 WebJob SDK를 사용하는 간단한 다중 계층 응용 프로그램을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-450">In this tutorial, you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="41501-451">이 섹션에서는 ASP.NET 다중 계층 응용 프로그램 및 Webjob에 대해 더 알아볼 몇 가지 제안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="41501-452">누락된 기능</span><span class="sxs-lookup"><span data-stu-id="41501-452">Missing features</span></span>
<span data-ttu-id="41501-453">이 응용 프로그램은 시작 자습서용으로 단순하게 유지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-453">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="41501-454">실제 응용 프로그램에서는 [종속성 주입](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) 또는 [리포지토리 및 작업 단위 패턴](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)을 구현하지 않고 [로깅용 인터페이스](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log)를 사용하며 데이터 모델 변경을 관리하는 데 [EF Code First 마이그레이션](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)을 사용하고 일시적인 네트워크 오류를 관리하는 데 [EF 연결 복원](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="41501-455">WebJob 크기 조정</span><span class="sxs-lookup"><span data-stu-id="41501-455">Scaling WebJobs</span></span>
<span data-ttu-id="41501-456">WebJob은 웹앱의 컨텍스트에서 실행되며 별도로 확장 가능하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-456">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="41501-457">예를 들어 표준 웹앱의 인스턴스가 하나 있으면 실행 중인 백그라운드 프로세스 인스턴스가 하나만 있고 웹 콘텐츠를 제공하는 데 사용될 수 있는 일부 서버 리소스(CPU, 메모리 등)를 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="41501-458">트래픽이 하루 중 시간이나 주중 요일별로 다르고 수행해야 하는 백 엔드 처리가 대기될 수 있는 경우 트래픽이 낮은 시간에 WebJob이 실행되도록 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-458">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="41501-459">부하가 여전히 해당 솔루션에 대해 너무 높은 경우 백 엔드를 해당 용도에 전용된 별도 웹앱에서 WebJob으로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-459">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="41501-460">그런 후 프런트 엔드 웹앱과는 별도로 백 엔드 웹앱을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="41501-461">자세한 내용은 [WebJob 확장](websites-webjobs-resources.md#scale)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="41501-462">웹앱 시간 제한 종료 방지</span><span class="sxs-lookup"><span data-stu-id="41501-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="41501-463">WebJob이 항상 실행되고 웹앱의 모든 인스턴스에서 실행되도록 하려면 [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-463">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="41501-464">WebJob 외부에서 WebJob SDK 사용</span><span class="sxs-lookup"><span data-stu-id="41501-464">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="41501-465">WebJob SDK를 사용하는 프로그램은 WebJob의 Azure에서 실행될 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-465">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="41501-466">로컬에서 실행할 수 있고 클라우드 서비스 작업자 역할 또는 Windows 서비스와 같은 다른 환경에서도 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="41501-467">하지만 WebJob SDK 대시보드에는 Azure 웹앱을 통해서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-467">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="41501-468">이 대시보드를 사용하려면 클래식 포털의 **구성** 탭에서 AzureWebJobsDashboard 연결 문자열을 설정하여 사용 중인 저장소 계정에 웹앱을 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41501-468">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="41501-469">그런 후 다음 URL을 사용하여 대시보드로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41501-469">Then, you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="41501-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span><span class="sxs-lookup"><span data-stu-id="41501-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="41501-471">자세한 내용은 [WebJobs SDK를 사용한 로컬 개발을 위해 대시보드 가져오기](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx)(영문)를 참조하세요. 단 여기에는 이전 연결 문자열 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="41501-471">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="41501-472">더 자세한 WebJob 설명서</span><span class="sxs-lookup"><span data-stu-id="41501-472">More WebJobs documentation</span></span>
<span data-ttu-id="41501-473">자세한 내용은 [Azure WebJob 설명서 리소스](http://go.microsoft.com/fwlink/?LinkId=390226)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="41501-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
