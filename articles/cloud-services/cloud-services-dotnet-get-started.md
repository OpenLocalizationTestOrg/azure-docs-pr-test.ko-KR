---
title: "Azure Cloud Services 및 ASP.NET 시작 | Microsoft 문서"
description: "ASP.NET MVC 및 Azure를 사용하여 다중 계층 앱을 만드는 방법을 알아보세요. 이 앱은 웹 역할 및 작업자 역할을 사용하여 클라우드 서비스에서 실행되며 Entity Framework, SQL 데이터베이스 및 Azure 저장소 큐와 Blob를 사용합니다."
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
ms.openlocfilehash: d2c197db73477d06d86d1c4faa8c4a2f58c7b391
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="56f65-105">Azure 클라우드 서비스 및 ASP.NET 시작</span><span class="sxs-lookup"><span data-stu-id="56f65-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="56f65-106">개요</span><span class="sxs-lookup"><span data-stu-id="56f65-106">Overview</span></span>
<span data-ttu-id="56f65-107">이 자습서에서는 ASP.NET MVC 프런트 엔드를 사용하여 다중 계층 .NET 응용 프로그램을 만들어 [Azure 클라우드 서비스](cloud-services-choose-me.md)에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-107">This tutorial shows how to create a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it to an [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="56f65-108">이 응용 프로그램은 [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)(영문) 및 [Azure 큐 서비스](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-108">The application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), the [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and the [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="56f65-109">MSDN 코드 갤러리에서 [Visual Studio 프로젝트를 다운로드](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-109">You can [download the Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from the MSDN Code Gallery.</span></span>

<span data-ttu-id="56f65-110">이 자습서에서는 응용 프로그램을 구축하고 로컬에서 실행하는 방법, 응용 프로그램을 Azure에 배포하고 클라우드에서 실행하는 방법, 그리고 응용 프로그램을 처음부터 구축하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-110">The tutorial shows you how to build and run the application locally, how to deploy it to Azure and run in the cloud, and how to build it from scratch.</span></span> <span data-ttu-id="56f65-111">처음부터 구축하는 방법으로 시작한 다음 원하는 경우 나중에 테스트 및 배포 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-111">You can start by building from scratch and then do the test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="56f65-112">Contoso Ads 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="56f65-112">Contoso Ads application</span></span>
<span data-ttu-id="56f65-113">응용 프로그램은 광고 게시판입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-113">The application is an advertising bulletin board.</span></span> <span data-ttu-id="56f65-114">사용자는 텍스트를 입력하고 이미지를 업로드하여 광고를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="56f65-115">사용자는 썸네일 이미지로 광고 목록을 볼 수 있으며 자세한 내용을 확인하기 위해 광고를 선택하면 전체 크기 이미지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-115">They can see a list of ads with thumbnail images, and they can see the full-size image when they select an ad to see the details.</span></span>

![광고 목록](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="56f65-117">이 응용 프로그램에서는 [큐 중심 작업 패턴](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) 을 사용하여 미리 보기를 만드는 CPU 사용량이 많은 작업을 백 엔드 프로세스에 오프로드합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-117">The application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="56f65-118">대체 아키텍처: 웹 사이트 및 WebJobs</span><span class="sxs-lookup"><span data-stu-id="56f65-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="56f65-119">이 자습서에서는 Azure 클라우드 서비스에서 프런트 엔드 및 백 엔드를 실행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-119">This tutorial shows how to run both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="56f65-120">대안은 [Azure 웹 사이트](/services/web-sites/)(영문)에서 프런트 엔드를 실행하고 백 엔드에 [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226)(영문) 기능(현재 미리 보기에서 제공)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-120">An alternative is to run the front-end in an [Azure website](/services/web-sites/) and use the [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for the back-end.</span></span> <span data-ttu-id="56f65-121">WebJobs를 사용하는 자습서는 [Azure WebJobs SDK 시작](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-121">For a tutorial that uses WebJobs, see [Get Started with the Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="56f65-122">시나리오에 가장 적합한 서비스를 선택하는 방법에 대한 자세한 내용은 [Azure 웹 사이트, 클라우드 서비스 및 가상 컴퓨터 비교](../app-service-web/choose-web-site-cloud-service-vm.md)(영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-122">For information about how to choose the services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="56f65-123">학습할 내용</span><span class="sxs-lookup"><span data-stu-id="56f65-123">What you'll learn</span></span>
* <span data-ttu-id="56f65-124">Azure SDK를 설치하여 사용자 컴퓨터에서 Azure를 개발할 수 있도록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="56f65-124">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="56f65-125">ASP.NET MVC 웹 역할 및 두 개의 작업자 역할을 사용하여 Visual Studio 클라우드 서비스 프로젝트를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="56f65-125">How to create a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="56f65-126">Azure 저장소 에뮬레이터를 사용하여 클라우드 서비스 프로젝트를 로컬에서 테스트하는 방법</span><span class="sxs-lookup"><span data-stu-id="56f65-126">How to test the cloud service project locally, using the Azure storage emulator.</span></span>
* <span data-ttu-id="56f65-127">Azure 클라우드 서비스에 클라우드 프로젝트를 게시하고 Azure 저장소 계정을 사용하여 테스트하는 방법</span><span class="sxs-lookup"><span data-stu-id="56f65-127">How to publish the cloud project to an Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="56f65-128">파일을 업로드하고 Azure Blob 서비스에 저장하는 방법</span><span class="sxs-lookup"><span data-stu-id="56f65-128">How to upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="56f65-129">계층 간 통신에 Azure 큐 서비스를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="56f65-129">How to use the Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56f65-130">필수 조건</span><span class="sxs-lookup"><span data-stu-id="56f65-130">Prerequisites</span></span>
<span data-ttu-id="56f65-131">이 자습서에서는 *웹 역할* 및 *작업자 역할* 용어와 같이 [Azure Cloud Services에 대한 기본 개념](cloud-services-choose-me.md)을 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-131">The tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="56f65-132">또한 Visual Studio에서 [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)(영문) 또는 [웹 양식](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview)(영문) 프로젝트를 작업하는 방법도 알고 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-132">It also assumes that you know how to work with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="56f65-133">응용 프로그램 예제는 MVC를 사용하지만, 자습서 내용의 대부분은 Web Forms에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-133">The sample application uses MVC, but most of the tutorial also applies to Web Forms.</span></span>

<span data-ttu-id="56f65-134">Azure 구독 없이도 로컬에서 앱을 실행할 수 있지만 응용 프로그램을 클라우드에 배포하려면 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-134">You can run the app locally without an Azure subscription, but you'll need one to deploy the application to the cloud.</span></span> <span data-ttu-id="56f65-135">계정이 없는 경우 [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668)하거나 [무료 평가판을 등록](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="56f65-136">자습서의 지침은 다음 제품 중 하나에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-136">The tutorial instructions work with either of the following products:</span></span>

* <span data-ttu-id="56f65-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="56f65-137">Visual Studio 2013</span></span>
* <span data-ttu-id="56f65-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="56f65-138">Visual Studio 2015</span></span>
* <span data-ttu-id="56f65-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="56f65-139">Visual Studio 2017</span></span>

<span data-ttu-id="56f65-140">위 제품 중 하나도 없는 경우 Azure SDK를 설치하면 Visual Studio가 자동으로 설치될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-140">If you don't have one of these, Visual Studio may be installed automatically when you install the Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="56f65-141">응용 프로그램 아키텍처</span><span class="sxs-lookup"><span data-stu-id="56f65-141">Application architecture</span></span>
<span data-ttu-id="56f65-142">앱은 Entity Framework Code First를 사용해 SQL 데이터베이스에 광고를 저장하여 테이블을 만들고 데이터에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-142">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="56f65-143">광고별로 데이터베이스는 전체 크기 이미지용과 썸네일용으로 두 개의 URL을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-143">For each ad, the database stores two URLs, one for the full-size image and one for the thumbnail.</span></span>

![광고 테이블](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="56f65-145">사용자가 이미지를 업로드하면 웹 역할로 실행 중인 프런트 엔드가 [Azure Blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)(영문)에 이미지를 저장하며 Blob을 가리키는 URL을 사용하여 데이터베이스에 광고 정보를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-145">When a user uploads an image, the front-end running in a web role stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="56f65-146">이와 동시에 Azure 큐에 메시지를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-146">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="56f65-147">작업자 역할로 실행되는 백 엔드 프로세스는 정기적으로 큐를 폴링하여 새 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-147">A back-end process running in a worker role periodically polls the queue for new messages.</span></span> <span data-ttu-id="56f65-148">새 메시지가 나타나면 작업자 역할은 해당 이미지의 미리 보기를 만들고 광고에 대한 미리 보기 URL 데이터베이스 필드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-148">When a new message appears, the worker role creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="56f65-149">다음은 응용 프로그램의 여러 부분이 상호 작용하는 방법을 보여 주는 다이어그램입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-149">The following diagram shows how the parts of the application interact.</span></span>

![Contoso Ads 아키텍처](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-the-completed-solution"></a><span data-ttu-id="56f65-151">완료된 솔루션 다운로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="56f65-151">Download and run the completed solution</span></span>
1. <span data-ttu-id="56f65-152">[완료된 솔루션](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)을 다운로드하고 압축 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-152">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="56f65-153">Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="56f65-154">**파일** 메뉴에서 **프로젝트 열기**를 선택하고 솔루션을 다운로드한 위치로 이동한 후 솔루션 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-154">From the **File** menu choose **Open Project**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="56f65-155">Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-155">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="56f65-156">기본적으로 Visual Studio는 *.zip* 파일에 포함되지 않은 NuGet 패키지 콘텐츠를 자동으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-156">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="56f65-157">패키지가 복원되지 않는 경우 **솔루션의 NuGet 패키지 관리** 대화 상자로 이동하고 오른쪽 위에서 **복원** 단추를 클릭하여 수동으로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-157">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog box and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="56f65-158">**솔루션 탐색기**에서 시작 프로젝트로 **ContosoAdsCloudService**가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as the startup project.</span></span>
6. <span data-ttu-id="56f65-159">Visual Studio 2015 이상을 사용하는 경우 ContosoAdsWeb 프로젝트의 응용 프로그램 *Web.config* 파일 및 ContosoAdsCloudService 프로젝트의 *ServiceConfiguration.Local.cscfg* 파일에서 SQL Server 연결 문자열을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-159">If you're using Visual Studio 2015 or higher, change the SQL Server connection string in the application *Web.config* file of the ContosoAdsWeb project and in the *ServiceConfiguration.Local.cscfg* file of the ContosoAdsCloudService project.</span></span> <span data-ttu-id="56f65-160">각각의 경우에서 "(localdb)\v11.0"을 "(localdb)\MSSQLLocalDB"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-160">In each case, change "(localdb)\v11.0" to "(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="56f65-161">Ctrl+F5를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-161">Press CTRL+F5 to run the application.</span></span>

    <span data-ttu-id="56f65-162">클라우드 서비스 프로젝트를 로컬에서 실행하면 Visual Studio는 Azure *계산 에뮬레이터* 및 Azure *저장소 에뮬레이터*를 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-162">When you run a cloud service project locally, Visual Studio automatically invokes the Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="56f65-163">계산 에뮬레이터는 컴퓨터의 리소스를 사용하여 웹 역할 및 작업자 역할 환경을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-163">The compute emulator uses your computer's resources to simulate the web role and worker role environments.</span></span> <span data-ttu-id="56f65-164">저장소 에뮬레이터는 [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) 데이터베이스를 사용하여 Azure 클라우드 저장소를 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-164">The storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database to simulate Azure cloud storage.</span></span>

    <span data-ttu-id="56f65-165">클라우드 서비스 프로젝트를 처음 실행하면 에뮬레이터가 시작되는 데 1분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-165">The first time you run a cloud service project, it takes a minute or so for the emulators to start up.</span></span> <span data-ttu-id="56f65-166">에뮬레이터 시작이 완료되면 기본 브라우저가 열려 응용 프로그램 홈페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-166">When emulator startup is finished, the default browser opens to the application home page.</span></span>

    ![Contoso Ads 아키텍처](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="56f65-168">**광고 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="56f65-169">일부 테스트 데이터를 입력하고 업로드할 *.jpg* 이미지를 선택한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-169">Enter some test data and select a *.jpg* image to upload, and then click **Create**.</span></span>

    ![만들기 페이지](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="56f65-171">앱이 인덱스 페이지로 이동하지만 아직 처리가 이루어지지 않았기 때문에 새 광고에 대한 미리 보기를 표시하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-171">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="56f65-172">잠깐 기다렸다가 인덱스 페이지를 새로 고쳐 미리 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-172">Wait a moment and then refresh the Index page to see the thumbnail.</span></span>

     ![인덱스 페이지](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="56f65-174">광고에 해당하는 **자세히** 를 클릭하여 전체 크기 이미지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-174">Click **Details** for your ad to see the full-size image.</span></span>

     ![자세히 페이지](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="56f65-176">클라우드 연결 없이 응용 프로그램을 전적으로 로컬 컴퓨터에서 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-176">You've been running the application entirely on your local computer, with no connection to the cloud.</span></span> <span data-ttu-id="56f65-177">저장소 에뮬레이터는 큐 및 Blob 데이터를 SQL Server Express LocalDB 데이터베이스에 저장하고, 응용 프로그램은 다른 LocalDB 데이터베이스에 광고 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-177">The storage emulator stores the queue and blob data in a SQL Server Express LocalDB database, and the application stores the ad data in another LocalDB database.</span></span> <span data-ttu-id="56f65-178">웹 앱이 처음으로 액세스하려고 시도했을 때 Entity Framework Code First는 자동으로 광고 데이터베이스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-178">Entity Framework Code First automatically created the ad database the first time the web app tried to access it.</span></span>

<span data-ttu-id="56f65-179">다음 섹션에서는 솔루션이 클라우드에서 실행될 때 큐, Blob 및 응용 프로그램 데이터베이스에 대해 Azure 클라우드 리소스를 사용하도록 솔루션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-179">In the following section you'll configure the solution to use Azure cloud resources for queues, blobs, and the application database when it runs in the cloud.</span></span> <span data-ttu-id="56f65-180">로컬에서 계속 실행하고 클라우드 저장소 및 데이터베이스 리소스를 사용하려면 그렇게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-180">If you wanted to continue to run locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="56f65-181">어떻게 할지는 연결 문자열을 설정하기에 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-181">It's just a matter of setting connection strings, which you'll see how to do.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="56f65-182">Azure에 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="56f65-182">Deploy the application to Azure</span></span>
<span data-ttu-id="56f65-183">클라우드에서 응용 프로그램을 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-183">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="56f65-184">Azure 클라우드 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="56f65-185">Azure SQL 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="56f65-186">Azure 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="56f65-187">Azure에서 실행될 때 Azure SQL 데이터베이스를 사용하도록 솔루션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-187">Configure the solution to use your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="56f65-188">Azure에서 실행될 때 Azure 저장소 계정을 사용하도록 솔루션을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-188">Configure the solution to use your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="56f65-189">Azure 클라우드 서비스에 프로젝트를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-189">Deploy the project to your Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="56f65-190">Azure 클라우드 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="56f65-190">Create an Azure cloud service</span></span>
<span data-ttu-id="56f65-191">Azure 클라우드 서비스는 응용 프로그램이 실행되는 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-191">An Azure cloud service is the environment the application will run in.</span></span>

1. <span data-ttu-id="56f65-192">브라우저에서 [Azure Portal](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-192">In your browser, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="56f65-193">**새로 만들기 > Compute > Cloud Service**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="56f65-194">DNS 이름 입력 상자에 클라우드 서비스의 URL 접두사를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-194">In the DNS name input box, enter a URL prefix for the cloud service.</span></span>

    <span data-ttu-id="56f65-195">이 URL은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-195">This URL has to be unique.</span></span>  <span data-ttu-id="56f65-196">선택한 접두사를 이미 사용 중이면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-196">You'll get an error message if the prefix you choose is already in use.</span></span>
4. <span data-ttu-id="56f65-197">서비스에 대한 새 리소스 그룹을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-197">Specify a new Resource group for the  service.</span></span> <span data-ttu-id="56f65-198">**새로 만들기**를 클릭한 다음 리소스 그룹 입력 상자에 이름(예: CS_contososadsRG)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-198">Click **Create new** and then type a name in the Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="56f65-199">응용 프로그램을 배포할 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-199">Choose the region where you want to deploy the application.</span></span>

    <span data-ttu-id="56f65-200">이 필드는 클라우드 서비스가 호스팅될 데이터센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="56f65-201">프로덕션 응용 프로그램의 경우 고객에게 가장 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-201">For a production application, you'd choose the region closest to your customers.</span></span> <span data-ttu-id="56f65-202">이 자습서에서는 자신에게 가장 가까운 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-202">For this tutorial, choose the region closest to you.</span></span>
5. <span data-ttu-id="56f65-203">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-203">Click **Create**.</span></span>

    <span data-ttu-id="56f65-204">다음 이미지에서는 CSvccontosoads.cloudapp.net이라는 URL로 클라우드 서비스가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-204">In the following image, a cloud service is created with the URL CSvccontosoads.cloudapp.net.</span></span>

    ![새 클라우드 서비스](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="56f65-206">Azure SQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="56f65-206">Create an Azure SQL database</span></span>
<span data-ttu-id="56f65-207">앱이 클라우드에서 실행될 때는 클라우드 기반 데이터베이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-207">When the app runs in the cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="56f65-208">[Azure Portal](https://portal.azure.com)에서 **새로 만들기 > 데이터베이스 > SQL Database**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-208">In the [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="56f65-209">**데이터베이스 이름** 상자에 *contosoads*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-209">In the **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="56f65-210">**리소스 그룹**에서 **기존 그룹 사용**을 클릭하고 클라우드 서비스에 사용된 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-210">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
4. <span data-ttu-id="56f65-211">다음 이미지에서 **서버 - 필수 설정 구성** 및 **새 서버 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-211">In the following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![데이터베이스 서버로 터널링](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="56f65-213">또는 이미 구독에 서버가 있는 경우에는 드롭다운 목록에서 해당 서버를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-213">Alternatively, if your subscription already has a server, you can select that server from the drop-down list.</span></span>
5. <span data-ttu-id="56f65-214">**서버 이름** 상자에 *csvccontosodbserver*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-214">In the **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="56f65-215">관리자 **로그인 이름** 및 **암호**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="56f65-216">**새 서버 만들기**를 선택한 경우 여기에 기존 이름 및 암호를 입력하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="56f65-217">나중에 데이터베이스에 액세스할 때 사용할 새 이름과 암호를 입력해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-217">You're entering a new name and password that you're defining now to use later when you access the database.</span></span> <span data-ttu-id="56f65-218">이전에 만든 서버를 선택한 경우 이미 만든 관리자 계정에 대한 암호를 입력하라는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-218">If you selected a server that you created previously, you'll be prompted for the password to the administrative user account you already created.</span></span>
7. <span data-ttu-id="56f65-219">클라우드 서비스에 선택한 것과 동일한 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-219">Choose the same **Location** that you chose for the cloud service.</span></span>

    <span data-ttu-id="56f65-220">클라우드 서비스와 데이터베이스가 서로 다른 데이터 센터, 즉 서로 다른 지역에 있는 경우 대기 시간이 길어지고 데이터 센터 외부 대역폭에 대한 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-220">When the cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="56f65-221">데이터 센터 내부 대역폭은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="56f65-222">**Azure 서비스의 서버 액세스 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-222">Check **Allow azure services to access server**.</span></span>
9. <span data-ttu-id="56f65-223">새 서버에 대해 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-223">Click **Select** for the new server.</span></span>

    ![새 SQL Database 서버](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="56f65-225">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="56f65-226">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="56f65-226">Create an Azure storage account</span></span>
<span data-ttu-id="56f65-227">Azure 저장소 계정은 큐 및 Blob 데이터를 클라우드에 저장하기 위한 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-227">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span>

<span data-ttu-id="56f65-228">실제 응용 프로그램에서는 일반적으로 응용 프로그램 데이터와 로깅 데이터를 위한 별도의 계정 및 테스트 데이터와 프로덕션 데이터를 위한 별도의 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="56f65-229">이 자습서에서는 하나의 계정만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="56f65-230">[Azure Portal](https://portal.azure.com)에서 **새로 만들기 > Storage > 저장소 계정 -Blob, 파일, 테이블, 큐**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-230">In the [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="56f65-231">**이름** 상자에 URL 접두사를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-231">In the **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="56f65-232">이 접두사와 상자 아래에 표시되는 텍스트가 저장소 계정의 고유 URL이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-232">This prefix plus the text you see under the box will be the unique URL to your storage account.</span></span> <span data-ttu-id="56f65-233">입력한 접두사를 이미 다른 사람이 사용하는 경우 다른 접두사를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-233">If the prefix you enter has already been used by someone else, you'll have to choose a different prefix.</span></span>
3. <span data-ttu-id="56f65-234">**배포 모델**을 *클래식*으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-234">Set the **Deployment model** to *Classic*.</span></span>

4. <span data-ttu-id="56f65-235">**복제** 드롭다운 목록을 **로컬 중복 저장소**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-235">Set the **Replication** drop-down list to **Locally redundant storage**.</span></span>

    <span data-ttu-id="56f65-236">저장소 계정에 대해 지역에서 복제를 사용하는 경우 저장된 콘텐츠가 보조 데이터 센터에 복제되어 기본 위치에서 대규모 재해가 발생하면 장애 조치(Failover)가 가능해집니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-236">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover if a major disaster occurs in the primary location.</span></span> <span data-ttu-id="56f65-237">지역에서 복제는 추가 비용을 발생시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="56f65-238">테스트 및 개발 계정의 경우 일반적으로 지역에서 복제 비용을 지불하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-238">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="56f65-239">자세한 내용은 [저장소 계정 만들기, 관리 또는 삭제](../storage/common/storage-create-storage-account.md)를 참조하세요</span><span class="sxs-lookup"><span data-stu-id="56f65-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="56f65-240">**리소스 그룹**에서 **기존 그룹 사용**을 클릭하고 클라우드 서비스에 사용된 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-240">In the **Resource group**, click **Use existing** and select the resource group used for the cloud service.</span></span>
6. <span data-ttu-id="56f65-241">**위치** 드롭다운 목록을 클라우드 서비스에 선택한 것과 동일한 지역으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-241">Set the **Location** drop-down list to the same region you chose for the cloud service.</span></span>

    <span data-ttu-id="56f65-242">클라우드 서비스와 저장소 계정이 서로 다른 데이터 센터, 즉 서로 다른 지역에 있는 경우 대기 시간이 길어지고 데이터 센터 외부 대역폭에 대한 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-242">When the cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside the data center.</span></span> <span data-ttu-id="56f65-243">데이터 센터 내부 대역폭은 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="56f65-244">Azure 선호도 그룹은 데이터 센터 리소스 사이의 거리를 최소화하는 메커니즘을 제공하며, 이로 인해 대기 시간이 줄어들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-244">Azure affinity groups provide a mechanism to minimize the distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="56f65-245">이 자습서는 선호도 그룹을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="56f65-246">자세한 내용은 [Azure에서 선호도 그룹을 만드는 방법](http://msdn.microsoft.com/library/jj156209.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-246">For more information, see [How to Create an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="56f65-247">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-247">Click **Create**.</span></span>

    ![새 저장소 계정](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="56f65-249">이미지에서 다음 URL을 사용하여 저장소 계정이 생성됩니다. `csvccontosoads.core.windows.net`</span><span class="sxs-lookup"><span data-stu-id="56f65-249">In the image, a storage account is created with the URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-the-solution-to-use-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="56f65-250">Azure에서 실행될 때 Azure SQL 데이터베이스를 사용하도록 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="56f65-250">Configure the solution to use your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="56f65-251">웹 프로젝트 및 작업자 역할 프로젝트는 각각 고유한 데이터베이스 연결 문자열을 가지며 앱이 Azure에서 실행될 때 Azure SQL 데이터베이스를 가리켜야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-251">The web project and the worker role project each has its own database connection string, and each needs to point to the Azure SQL database when the app runs in Azure.</span></span>

<span data-ttu-id="56f65-252">웹 역할에 대해 [Web.config 변환](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) (영문)을 사용하고 작업자 역할에 대해 클라우드 서비스 환경 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for the web role and a cloud service environment setting for the worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="56f65-253">이 섹션 및 다음 섹션에서는 프로젝트 파일에 자격 증명을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-253">In this section and the next section, you store credentials in project files.</span></span> <span data-ttu-id="56f65-254">[중요한 데이터를 공개 소스 코드 리포지토리에 저장하지 마세요](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets)(영문).</span><span class="sxs-lookup"><span data-stu-id="56f65-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="56f65-255">ContosoAdsWeb 프로젝트에서 응용 프로그램 *Web.config* 파일에 대한 *Web.Release.config* 변환 파일을 열고 `<connectionStrings>` 요소가 포함된 주석 블록을 삭제한 후 그 자리에 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-255">In the ContosoAdsWeb project, open the *Web.Release.config* transform file for the application *Web.config* file, delete the comment block that contains a `<connectionStrings>` element, and paste the following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="56f65-256">편집용으로 파일을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-256">Leave the file open for editing.</span></span>
2. <span data-ttu-id="56f65-257">[Azure Portal](https://portal.azure.com)에서 왼쪽 창의 **SQL Database**를 클릭하고 이 자습서에 대해 만든 데이터베이스를 클릭한 후 **연결 문자열 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-257">In the [Azure portal](https://portal.azure.com), click **SQL Databases** in the left pane, click the database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![연결 문자열 표시](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="56f65-259">포털은 암호 자리 표시자가 포함된 연결 문자열을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-259">The portal displays connection strings, with a placeholder for the password.</span></span>

    ![연결 문자열](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="56f65-261">*Web.Release.config* 변환 파일에서 `{connectionstring}`을 삭제한 후 그 자리에 Azure Portal에서 가져온 ADO.NET 연결 문자열을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-261">In the *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place the ADO.NET connection string from the Azure portal.</span></span>
4. <span data-ttu-id="56f65-262">*Web.Release.config* 변환 파일에 붙여 넣은 연결 문자열에서 `{your_password_here}` 대신 새 SQL 데이터베이스에 대해 만든 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-262">In the connection string that you pasted into the *Web.Release.config* transform file, replace `{your_password_here}` with the password you created for the new SQL database.</span></span>
5. <span data-ttu-id="56f65-263">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-263">Save the file.</span></span>  
6. <span data-ttu-id="56f65-264">작업자 역할 프로젝트를 구성하는 다음 단계에서 사용할 수 있도록 연결 문자열을 선택하고 복사합니다(둘러싼 따옴표 미포함).</span><span class="sxs-lookup"><span data-stu-id="56f65-264">Select and copy the connection string (without the surrounding quotation marks) for use in the following steps for configuring the worker role project.</span></span>
7. <span data-ttu-id="56f65-265">**솔루션 탐색기**에서, 클라우드 서비스 프로젝트의 **역할** 아래에서 **ContosoAdsWorker**를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-265">In **Solution Explorer**, under **Roles** in the cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![역할 속성](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="56f65-267">**설정** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-267">Click the **Settings** tab.</span></span>
9. <span data-ttu-id="56f65-268">**서비스 구성**을 **클라우드**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-268">Change **Service Configuration** to **Cloud**.</span></span>
10. <span data-ttu-id="56f65-269">`ContosoAdsDbConnectionString` 설정에서 **값** 필드를 선택한 다음 자습서의 이전 섹션에서 복사한 연결 문자열을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-269">Select the **Value** field for the `ContosoAdsDbConnectionString` setting, and then paste the connection string that you copied from the previous section of the tutorial.</span></span>

     ![작업자 역할의 데이터베이스 연결 문자열](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="56f65-271">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-271">Save your changes.</span></span>  

### <a name="configure-the-solution-to-use-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="56f65-272">Azure에서 실행될 때 Azure 저장소 계정을 사용하도록 솔루션 구성</span><span class="sxs-lookup"><span data-stu-id="56f65-272">Configure the solution to use your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="56f65-273">웹 역할 프로젝트 및 작업자 역할 프로젝트에 대한 Azure 저장소 계정 연결 문자열은 클라우드 서비스 프로젝트의 환경 설정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-273">Azure storage account connection strings for both the web role project and the worker role project are stored in environment settings in the cloud service project.</span></span> <span data-ttu-id="56f65-274">각 프로젝트에는 응용 프로그램이 로컬에서 실행될 때와 클라우드에서 실행될 때 사용되는 별도의 설정 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-274">For each project, there is a separate set of settings to be used when the application runs locally and when it runs in the cloud.</span></span> <span data-ttu-id="56f65-275">웹 역할 및 작업자 역할 프로젝트의 클라우드 환경 설정을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-275">You'll update the cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="56f65-276">**솔루션 탐색기**에서 **ContosoAdsCloudService** 프로젝트의 **역할** 아래에 있는 **ContosoAdsWeb**을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in the **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![역할 속성](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="56f65-278">**설정** 탭을 클릭합니다. **서비스 구성** 드롭다운 상자에서 **클라우드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-278">Click the **Settings** tab. In the **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![클라우드 구성](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="56f65-280">**StorageConnectionString** 항목을 선택하면 줄 오른쪽 끝에 줄임표(**...**) 단추가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-280">Select the **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at the right end of the line.</span></span> <span data-ttu-id="56f65-281">줄임표 단추를 클릭하여 **저장소 계정 연결 문자열 만들기** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-281">Click the ellipsis button to open the **Create Storage Account Connection String** dialog box.</span></span>

    ![열린 연결 문자열 만들기 상자](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="56f65-283">**저장소 연결 문자열 만들기** 대화 상자에서 **내 구독**을 클릭하고, 앞에서 만든 저장소 계정을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-283">In the **Create Storage Connection String** dialog box, click **Your subscription**, choose the storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="56f65-284">아직 로그인하지 않은 경우 Azure 계정 자격 증명을 요구하는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![저장소 연결 문자열 만들기](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="56f65-286">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-286">Save your changes.</span></span>
6. <span data-ttu-id="56f65-287">`StorageConnectionString` 연결 문자열에 사용한 것과 동일한 절차에 따라 `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` 연결 문자열을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-287">Follow the same procedure that you used for the `StorageConnectionString` connection string to set the `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="56f65-288">이 연결 문자열은 로깅에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="56f65-289">**ContosoAdsWeb** 역할에 사용한 것과 동일한 절차에 따라 **ContosoAdsWorker** 역할에 대한 연결 문자열을 모두 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-289">Follow the same procedure that you used for the **ContosoAdsWeb** role to set both connection strings for the **ContosoAdsWorker** role.</span></span> <span data-ttu-id="56f65-290">**서비스 구성**을 **클라우드**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-290">Don't forget to set **Service Configuration** to **Cloud**.</span></span>

<span data-ttu-id="56f65-291">Visual Studio UI를 사용하여 구성한 역할 환경 설정은 ContosoAdsCloudService 프로젝트에서 다음 파일에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-291">The role environment settings that you have configured using the Visual Studio UI are stored in the following files in the ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="56f65-292">*ServiceDefinition.csdef* - 설정 이름을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-292">*ServiceDefinition.csdef* - Defines the setting names.</span></span>
* <span data-ttu-id="56f65-293">*ServiceConfiguration.Cloud.cscfg* - 앱이 클라우드에서 실행되는 경우에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when the app runs in the cloud.</span></span>
* <span data-ttu-id="56f65-294">*ServiceConfiguration.Local.cscfg* - 앱이 로컬에서 실행되는 경우에 대한 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-294">*ServiceConfiguration.Local.cscfg* - Provides values for when the app runs locally.</span></span>

<span data-ttu-id="56f65-295">예를 들어 ServiceDefinition.csdef에는 다음 정의가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-295">For example, the ServiceDefinition.csdef includes the following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="56f65-296">그리고 *ServiceConfiguration.Cloud.cscfg* 파일에는 Visual Studio에서 해당 설정에 입력한 값이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-296">And the *ServiceConfiguration.Cloud.cscfg* file includes the values you entered for those settings in Visual Studio.</span></span>

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

<span data-ttu-id="56f65-297">`<Instances>` 설정은 Azure가 작업자 역할 코드를 실행할 가상 컴퓨터의 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-297">The `<Instances>` setting specifies the number of virtual machines that Azure will run the worker role code on.</span></span> <span data-ttu-id="56f65-298">[다음 단계](#next-steps) 섹션에는 클라우드 서비스 규모 확장에 대한 자세한 정보로 연결되는 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-298">The [Next steps](#next-steps) section includes links to more information about scaling out a cloud service,</span></span>

### <a name="deploy-the-project-to-azure"></a><span data-ttu-id="56f65-299">Azure에 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="56f65-299">Deploy the project to Azure</span></span>
1. <span data-ttu-id="56f65-300">**솔루션 탐색기**에서 **ContosoAdsCloudService** 클라우드 프로젝트를 마우스 오른쪽 단추로 클릭한 후 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-300">In **Solution Explorer**, right-click the **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![게시 메뉴](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="56f65-302">**Azure 응용 프로그램 게시** 마법사의 **로그인** 단계에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-302">In the **Sign in** step of the **Publish Azure Application** wizard, click **Next**.</span></span>

    ![로그인 단계](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="56f65-304">마법사의 **설정** 단계에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-304">In the **Settings** step of the wizard, click **Next**.</span></span>

    ![설정 단계](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="56f65-306">**고급** 탭의 기본 설정은 이 자습서 내용에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-306">The default settings in the **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="56f65-307">고급 탭에 대한 자세한 내용은 [Azure 응용 프로그램 게시 마법사](http://msdn.microsoft.com/library/hh535756.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-307">For information about the advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="56f65-308">**요약** 단계에서 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-308">In the **Summary** step, click **Publish**.</span></span>

    ![요약 단계](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="56f65-310">Visual Studio에서 **Azure 활동 로그** 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-310">The **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="56f65-311">오른쪽 화살표 아이콘을 클릭하여 배포 세부 정보를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-311">Click the right arrow icon to expand the deployment details.</span></span>

    <span data-ttu-id="56f65-312">배포가 완료되는 데 약 5분 이상 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-312">The deployment can take up to 5 minutes or more to complete.</span></span>

    ![Azure 활동 로그 창](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="56f65-314">배포 상태가 완료되면 **웹 앱 URL** 을 클릭하여 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-314">When the deployment status is complete, click the **Web app URL** to start the application.</span></span>
7. <span data-ttu-id="56f65-315">이제 응용 프로그램을 로컬에서 실행할 때처럼 일부 광고를 만들고, 보고, 편집하는 방법으로 앱을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-315">You can now test the app by creating, viewing, and editing some ads, as you did when you ran the application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="56f65-316">테스트를 완료하면 클라우드 서비스를 삭제하거나 중지하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-316">When you're finished testing, delete or stop the cloud service.</span></span> <span data-ttu-id="56f65-317">클라우드 서비스를 사용하지 않더라도 가상 컴퓨터 리소스가 예약되어 있기 때문에 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-317">Even if you're not using the cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="56f65-318">또한 실행 중인 채로 두는 경우에는 누군가가 URL을 발견하면 광고를 만들고 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="56f65-319">[Azure Portal](https://portal.azure.com)에서 클라우드 서비스의 **개요** 탭으로 이동한 다음 페이지 맨 위에 있는 **삭제** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-319">In the [Azure portal](https://portal.azure.com), go to the **Overview** tab for your cloud service, and then click the **Delete** button at the top of the page.</span></span> <span data-ttu-id="56f65-320">임시로 다른 사람이 사이트에 액세스하지 못하도록 만들려면 대신 **중지** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-320">If you just want to temporarily prevent others from accessing the site, click **Stop** instead.</span></span> <span data-ttu-id="56f65-321">이 경우에는 요금이 계속해서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-321">In that case, charges will continue to accrue.</span></span> <span data-ttu-id="56f65-322">더 이상 필요 없는 경우 비슷한 절차에 따라 SQL 데이터베이스 및 저장소 계정을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-322">You can follow a similar procedure to delete the SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-the-application-from-scratch"></a><span data-ttu-id="56f65-323">처음부터 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="56f65-323">Create the application from scratch</span></span>
<span data-ttu-id="56f65-324">아직 [완료된 응용 프로그램](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4)(영문)을 다운로드하지 않았다면 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-324">If you haven't already downloaded [the completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="56f65-325">다운로드한 프로젝트에서 새 프로젝트로 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-325">You'll copy files from the downloaded project into the new project.</span></span>

<span data-ttu-id="56f65-326">Contoso Ads 응용 프로그램을 만드는 데는 다음 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-326">Creating the Contoso Ads application involves the following steps:</span></span>

* <span data-ttu-id="56f65-327">클라우드 서비스 Visual Studio 솔루션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="56f65-328">NuGet 패키지를 업데이트 및 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="56f65-329">프로젝트 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-329">Set project references.</span></span>
* <span data-ttu-id="56f65-330">연결 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-330">Configure connection strings.</span></span>
* <span data-ttu-id="56f65-331">코드 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-331">Add code files.</span></span>

<span data-ttu-id="56f65-332">솔루션이 만들어진 후에는 클라우드 서비스 프로젝트에 고유한 코드와 Azure Blob 및 큐를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-332">After the solution is created, you'll review the code that is unique to cloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="56f65-333">클라우드 서비스 Visual Studio 솔루션 만들기</span><span class="sxs-lookup"><span data-stu-id="56f65-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="56f65-334">Visual Studio의 **새 프로젝트** from the **새 프로젝트** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-334">In Visual Studio, choose **New Project** from the **File** menu.</span></span>
2. <span data-ttu-id="56f65-335">**새 프로젝트** 대화 상자의 왼쪽 창에서 **Visual C#**을 확장하고 **클라우드** 템플릿을 선택한 후 **Azure 클라우드 서비스** 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-335">In the left pane of the **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose the **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="56f65-336">프로젝트 및 솔루션의 이름을 ContosoAdsCloudService로 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-336">Name the project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![새 프로젝트](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="56f65-338">**새 Azure 클라우드 서비스** 대화 상자에서 웹 역할 및 작업자 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-338">In the **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="56f65-339">웹 역할의 이름을 ContosoAdsWeb으로 지정하고 작업자 역할의 이름을 ContosoAdsWorker로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-339">Name the web role ContosoAdsWeb, and name the worker role ContosoAdsWorker.</span></span> <span data-ttu-id="56f65-340">(역할의 기본 이름을 변경하려면 오른쪽 창에 있는 연필 아이콘을 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="56f65-340">(Use the pencil icon in the right-hand pane to change the default names of the roles.)</span></span>

    ![새 클라우드 서비스 프로젝트](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="56f65-342">웹 역할에 대한 **새 ASP.NET 프로젝트** 대화 상자가 표시되면 MVC 템플릿을 선택하고 **인증 변경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-342">When you see the **New ASP.NET Project** dialog box for the web role, choose the MVC template, and then click **Change Authentication**.</span></span>

    ![인증 변경](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="56f65-344">**인증 변경** 대화 상자에서 **인증 없음**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-344">In the **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![인증 없음](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="56f65-346">**새 ASP.NET 프로젝트** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-346">In the **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="56f65-347">**솔루션 탐색기**에서 솔루션(프로젝트 중 하나가 아님)을 마우스 오른쪽 단추로 클릭하고 **추가 - 새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-347">In **Solution Explorer**, right-click the solution (not one of the projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="56f65-348">**새 프로젝트 추가** 대화 상자의 왼쪽 창에서 **Visual C#**에 있는 **Windows**을 선택한 다음 **클래스 라이브러리** 템플릿을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-348">In the **Add New Project** dialog box, choose **Windows** under **Visual C#** in the left pane, and then click the **Class Library** template.</span></span>  
10. <span data-ttu-id="56f65-349">프로젝트의 이름을 *ContosoAdsCommon*으로 지정한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-349">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="56f65-350">Entity Framework 컨텍스트 및 웹 역할 프로젝트와 작업자 역할 프로젝트의 데이터 모델을 참조해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-350">You need to reference the Entity Framework context and the data model from both web and worker role projects.</span></span> <span data-ttu-id="56f65-351">또는 웹 역할 프로젝트에서 EF 관련 클래스를 정의하고 작업자 역할 프로젝트에서 이 프로젝트를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-351">As an alternative, you could define the EF-related classes in the web role project and reference that project from the worker role project.</span></span> <span data-ttu-id="56f65-352">하지만 대안에서는 작업자 역할 프로젝트에는 필요 없는 웹 어셈블리 참조가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-352">But in the alternative approach, your worker role project would have a reference to web assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="56f65-353">NuGet 패키지 업데이트 및 추가</span><span class="sxs-lookup"><span data-stu-id="56f65-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="56f65-354">솔루션에 대한 **NuGet 패키지 관리** 대화 상자를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-354">Open the **Manage NuGet Packages** dialog box for the solution.</span></span>
2. <span data-ttu-id="56f65-355">창 맨 위에서 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-355">At the top of the window, select **Updates**.</span></span>
3. <span data-ttu-id="56f65-356">*WindowsAzure.Storage* 패키지를 찾고 목록에 있는 경우 선택합니다. 업데이트하려면 웹 및 작업자 프로젝트를 선택한 다음 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-356">Look for the *WindowsAzure.Storage* package, and if it's in the list, select it and select the web and worker projects to update it in, and then click **Update**.</span></span>

    <span data-ttu-id="56f65-357">저장소 클라이언트 라이브러리는 Visual Studio 프로젝트 템플릿보다 자주 업데이트됩니다. 따라서 새로 생성된 프로젝트에서 버전을 업데이트해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-357">The storage client library is updated more frequently than Visual Studio project templates, so you'll often find that the version in a newly-created project needs to be updated.</span></span>
4. <span data-ttu-id="56f65-358">창 맨 위에서 **찾아보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-358">At the top of the window, select **Browse**.</span></span>
5. <span data-ttu-id="56f65-359">*EntityFramework* NuGet 패키지를 찾아 세 개의 프로젝트 모두에서 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-359">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="56f65-360">*Microsoft.WindowsAzure.ConfigurationManager* NuGet 패키지를 찾은 후 작업자 역할 프로젝트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-360">Find the *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in the worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="56f65-361">프로젝트 참조 설정</span><span class="sxs-lookup"><span data-stu-id="56f65-361">Set project references</span></span>
1. <span data-ttu-id="56f65-362">ContosoAdsWeb 프로젝트에서 ContosoAdsCommon 프로젝트에 대한 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-362">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="56f65-363">ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **참조** - **참조 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-363">Right-click the ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="56f65-364">**참조 관리자** 대화 상자의 왼쪽 창에서 **솔루션 – 프로젝트**를 선택하고 **ContosoAdsCommon**을 선택한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-364">In the **Reference Manager** dialog box, select **Solution – Projects** in the left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="56f65-365">ContosoAdsWorker 프로젝트에서 ContosAdsCommon 프로젝트에 대한 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-365">In the ContosoAdsWorker project, set a reference to the ContosAdsCommon project.</span></span>

    <span data-ttu-id="56f65-366">ContosoAdsCommon에는 Entity Framework 데이터 모델 및 컨텍스트 클래스가 포함되며, 이는 프런트 엔드 및 백 엔드 모두에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-366">ContosoAdsCommon will contain the Entity Framework data model and context class, which will be used by both the front-end and back-end.</span></span>
3. <span data-ttu-id="56f65-367">ContosoAdsWorker 프로젝트에서 `System.Drawing`에 대한 참조를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-367">In the ContosoAdsWorker project, set a reference to `System.Drawing`.</span></span>

    <span data-ttu-id="56f65-368">이 어셈블리는 백 엔드에서 이미지를 미리 보기로 변환하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-368">This assembly is used by the back-end to convert images to thumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="56f65-369">연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="56f65-369">Configure connection strings</span></span>
<span data-ttu-id="56f65-370">이 섹션에서는 로컬 테스트를 위해 Azure Storage 및 SQL 연결 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="56f65-371">자습서 앞부분의 배포 지침에서는 앱이 클라우드에서 실행되는 경우를 위한 연결 문자열을 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-371">The deployment instructions earlier in the tutorial explain how to set up the connection strings for when the app runs in the cloud.</span></span>

1. <span data-ttu-id="56f65-372">ContosoAdsWeb 프로젝트에서 응용 프로그램 Web.config 파일을 열고 다음 `connectionStrings` 요소를 `configSections` 요소 뒤에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-372">In the ContosoAdsWeb project, open the application Web.config file, and insert the following `connectionStrings` element after the `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="56f65-373">Visual Studio 2015 이상을 사용하는 경우 "v11.0"을 "MSSQLLocalDB"로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="56f65-374">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-374">Save your changes.</span></span>
3. <span data-ttu-id="56f65-375">ContosoAdsCloudService 프로젝트에서 **역할**아래의 ContosoAdsWeb을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-375">In the ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![역할 속성](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="56f65-377">**ContosAdsWeb [Role]** 속성 창에서 **설정** 탭을 클릭한 다음 **설정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-377">In the **ContosAdsWeb [Role]** properties window, click the **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="56f65-378">**서비스 구성**을 **모든 구성**으로 설정해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-378">Leave **Service Configuration** set to **All Configurations**.</span></span>
5. <span data-ttu-id="56f65-379">이름이 *StorageConnectionString*인 설정을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="56f65-380">**형식**을 *ConnectionString*으로 설정하고 **값**을 *UseDevelopmentStorage=true*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-380">Set **Type** to *ConnectionString*, and set **Value** to *UseDevelopmentStorage=true*.</span></span>

    ![새 연결 문자열](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="56f65-382">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-382">Save your changes.</span></span>
7. <span data-ttu-id="56f65-383">동일한 절차에 따라 ContosoAdsWorker 역할 속성에서 저장소 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-383">Follow the same procedure to add a storage connection string in the ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="56f65-384">계속 **ContosoAdsWorker [Role]** 속성 창에서 다른 연결 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-384">Still in the **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="56f65-385">이름: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="56f65-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="56f65-386">형식: String</span><span class="sxs-lookup"><span data-stu-id="56f65-386">Type: String</span></span>
   * <span data-ttu-id="56f65-387">값: 웹 역할 프로젝트에 사용한 것과 동일한 연결 문자열을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-387">Value: Paste the same connection string you used for the web role project.</span></span> <span data-ttu-id="56f65-388">(다음은 Visual Studio 2013용 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-388">(The following example is for Visual Studio 2013.</span></span> <span data-ttu-id="56f65-389">이 예제를 복사하고 Visual Studio 2015 이상을 사용하는 경우 데이터 원본을 반드시 변경해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="56f65-389">Don't forget to change the Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="56f65-390">코드 파일 추가</span><span class="sxs-lookup"><span data-stu-id="56f65-390">Add code files</span></span>
<span data-ttu-id="56f65-391">이 섹션에서는 다운로드한 솔루션에서 새 솔루션으로 코드 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-391">In this section, you copy code files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="56f65-392">다음 섹션에서는 이 코드의 주요 부분을 보여 주고 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-392">The following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="56f65-393">프로젝트나 폴더에 파일을 추가하려면 프로젝트나 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** - **기존 항목**에 배포하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-393">To add files to a project or a folder, right-click the project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="56f65-394">원하는 파일을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-394">Select the files you want and then click **Add**.</span></span> <span data-ttu-id="56f65-395">기존 파일을 바꿀지 여부를 묻는 메시지가 나타나면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-395">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="56f65-396">ContosoAdsCommon 프로젝트에서 *Class1.cs* 파일을 삭제하고 그 자리에 다운로드한 프로젝트에서 가져온 *Ad.cs* 및 *ContosoAdscontext.cs* 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-396">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the *Ad.cs* and *ContosoAdscontext.cs* files from the downloaded project.</span></span>
2. <span data-ttu-id="56f65-397">ContosoAdsWeb 프로젝트에 다운로드한 프로젝트에서 가져온 다음 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-397">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="56f65-398">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="56f65-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="56f65-399">*Views\Shared* 폴더: *\__Layout.cshtml*</span><span class="sxs-lookup"><span data-stu-id="56f65-399">In the *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="56f65-400">*Views\Home* 폴더: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="56f65-400">In the *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="56f65-401">*Controllers* 폴더: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="56f65-401">In the *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="56f65-402">*Views\Ad* 폴더(먼저 폴더 만들기): 5개의 *.cshtml* 파일</span><span class="sxs-lookup"><span data-stu-id="56f65-402">In the *Views\Ad* folder (create the folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="56f65-403">ContosoAdsWorker 프로젝트에서 다운로드한 프로젝트에서 가져온 *WorkerRole.cs* 를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-403">In the ContosoAdsWorker project, add *WorkerRole.cs* from the downloaded project.</span></span>

<span data-ttu-id="56f65-404">이제 자습서 앞부분의 지침에 따라 응용 프로그램을 구축하고 실행할 수 있습니다. 앱은 로컬 데이터베이스 및 저장소 에뮬레이터 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-404">You can now build and run the application as instructed earlier in the tutorial, and the app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="56f65-405">다음 섹션에서는 Azure 환경, Blob 및 큐 작업과 관련된 코드에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-405">The following sections explain the code related to working with the Azure environment, blobs, and queues.</span></span> <span data-ttu-id="56f65-406">이 자습서에 스캐폴딩을 사용하여 MVC 컨트롤러 및 보기를 만드는 방법(영문), SQL Server 데이터베이스를 사용하는 Entity Framework 코드를 작성하는 방법(영문) 또는 ASP.NET 4.5의 비동기 프로그래밍에 대한 기본 사항(영문)은 나와 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-406">This tutorial does not explain how to create MVC controllers and views using scaffolding, how to write Entity Framework code that works with SQL Server databases, or the basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="56f65-407">이러한 항목에 대한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-407">For information about these topics, see the following resources:</span></span>

* [<span data-ttu-id="56f65-408">MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="56f65-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="56f65-409">EF 6 및 MVC 5 시작</span><span class="sxs-lookup"><span data-stu-id="56f65-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="56f65-410">[.NET 4.5의 비동기 프로그래밍 소개](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="56f65-410">[Introduction to asynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="56f65-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="56f65-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="56f65-412">Ad.cs 파일은 광고 범주의 열거형 및 광고 정보에 대한 POCO 엔터티 클래스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-412">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="56f65-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="56f65-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="56f65-414">ContosoAdsContext 클래스는 DbSet 컬렉션에서 Ad 클래스가 사용된다는 것을 지정하며, Entity Framework는 이를 SQL 데이터베이스에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-414">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

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

<span data-ttu-id="56f65-415">이 클래스에는 두 개의 생성자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-415">The class has two constructors.</span></span> <span data-ttu-id="56f65-416">첫 번째 생성자는 웹 프로젝트에서 사용되며 Web.config 파일에 저장되는 연결 문자열의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-416">The first of them is used by the web project, and specifies the name of a connection string that is stored in the Web.config file.</span></span> <span data-ttu-id="56f65-417">두 번째 생성자를 사용하면 Web.config 파일이 없으므로 작업자 역할 프로젝트에서 사용된 실제 연결 문자열을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-417">The second constructor enables you to pass in the actual connection string used by the worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="56f65-418">앞에서 이 연결 문자열이 저장된 위치를 확인했으며, 이후에 코드가 DbContext 클래스를 인스턴스화할 때 연결 문자열을 검색하는 방법을 확인하게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-418">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="56f65-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="56f65-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="56f65-420">`Application_Start` 메서드에서 호출되는 코드는 *images* Blob 컨테이너 및 *images* 큐를 만듭니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="56f65-420">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="56f65-421">따라서 새 저장소 계정을 사용하기 시작하거나 새 컴퓨터에서 저장소 에뮬레이터를 사용하기 시작할 때마다 필수 Blob 컨테이너와 큐가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-421">This ensures that whenever you start using a new storage account, or start using the storage emulator on a new computer, the required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="56f65-422">이 코드는 *.cscfg* 파일의 저장소 연결 문자열을 사용하여 저장소 계정에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-422">The code gets access to the storage account by using the storage connection string from the *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="56f65-423">그런 다음, *images* Blob 컨테이너에 대한 참조를 가져오고 컨테이너를 만들고(아직 없는 경우) 새 컨테이너에 대한 액세스 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-423">Then it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="56f65-424">기본적으로 새 컨테이너는 저장소 계정 자격 증명이 있는 클라이언트만 Blob에 액세스할 수 있게 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-424">By default, new containers only allow clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="56f65-425">이미지 Blob을 가리키는 URL을 사용하여 이미지를 표시할 수 있도록 웹 사이트는 Blob을 공개로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-425">The website needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="56f65-426">비슷한 코드가 *images* 큐에 대한 참조를 가져오고 새 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-426">Similar code gets a reference to the *images* queue and creates a new queue.</span></span> <span data-ttu-id="56f65-427">이런 경우 권한을 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="56f65-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="56f65-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="56f65-429">*_Layout.cshtml* 파일은 머리글과 바닥글에서 앱 이름을 설정하고 "Ads" 메뉴 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-429">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="56f65-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="56f65-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="56f65-431">*Views\Home\Index.cshtml* 파일은 홈페이지에 범주 링크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-431">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="56f65-432">이 링크는 쿼리 문자열 변수의 `Category` 열거형 정수 값을 광고 인덱스 페이지에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-432">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="56f65-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="56f65-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="56f65-434">*AdController.cs* 파일에서 생성자는 `InitializeStorage` 메서드를 호출하여 Blob 및 큐 작업을 위한 API를 제공하는 Azure Storage 클라이언트 라이브러리 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-434">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="56f65-435">그런 다음 이 코드는 앞서 *Global.asax.cs*에서 확인한 *images* Blob 컨테이너에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-435">Then the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="56f65-436">그 과정에서 웹앱에 해당하는 기본 [재시도 정책](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) (영문)을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="56f65-437">기본 지수 백오프 재시도 정책은 일시적 오류에 대해 반복적으로 재시도하는 경우 1분 넘게 웹앱을 중지시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-437">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="56f65-438">여기에 지정된 재시도 정책은 각 시도 후 3초 동안 최대 3회까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-438">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="56f65-439">비슷한 코드가 *images* 큐에 대한 참조를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-439">Similar code gets a reference to the *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="56f65-440">대부분의 컨트롤러 코드는 DbContext 클래스를 사용한 Entity Framework 데이터 모델 작업에 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-440">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="56f65-441">예외는 HttpPost `Create` 서드이며, 이 메서드는 파일을 업로드하고 Blob 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-441">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="56f65-442">모델 바인더는 메서드에 [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-442">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="56f65-443">사용자가 업로드할 파일을 선택한 경우 코드는 파일을 업로드하고 Blob에 저장하며 광고 데이터베이스 레코드를 Blob을 가리키는 URL로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-443">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="56f65-444">업로드를 수행하는 코드는 `UploadAndSaveBlobAsync` 메서드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-444">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="56f65-445">Blob에 대한 GUID 이름을 만들고, 파일을 업로드 및 저장하며, 저장된 Blob에 대한 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-445">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="56f65-446">HttpPost `Create` 메서드가 Blob을 업로드하고 데이터베이스를 업데이트한 후에는 이미지를 미리 보기로 변환할 수 있는 백 엔드 프로세스에 대해 알리는 큐 메시지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-446">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform that back-end process that an image is ready for conversion to a thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="56f65-447">HttpPost `Edit` 메서드의 코드도 비슷하지만, 사용자가 새 이미지 파일을 선택하면 이미 존재하는 Blob를 삭제해야 한다는 점은 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-447">The code for the HttpPost `Edit` method is similar except that if the user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="56f65-448">다음 예에서는 광고를 삭제하면 Blob을 삭제하는 코드를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-448">The next example shows the code that deletes blobs when you delete an ad.</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="56f65-449">ContosoAdsWeb - Views\Ad\Index.cshtml 및 Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="56f65-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="56f65-450">*Index.cshtml* 파일은 다른 광고 데이터가 포함된 미리 보기를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-450">The *Index.cshtml* file displays thumbnails with the other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="56f65-451">*Details.cshtml* 파일은 전체 크기 이미지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-451">The *Details.cshtml* file displays the full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="56f65-452">ContosoAdsWeb - Views\Ad\Create.cshtml 및 Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="56f65-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="56f65-453">*Create.cshtml* 및 *Edit.cshtml* 파일은 컨트롤러가 `HttpPostedFileBase` 개체를 가져올 수 있게 하는 양식 인코딩을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-453">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="56f65-454">`<input>` 요소는 파일 선택 대화 상자를 제공하도록 브라우저에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-454">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="56f65-455">ContosoAdsWorker - WorkerRole.cs - OnStart 메서드</span><span class="sxs-lookup"><span data-stu-id="56f65-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="56f65-456">Azure 작업자 역할 환경은 작업자 역할이 시작될 때 `OnStart` 메서드(`WorkerRole` 클래스에 있음)를 호출하고 `Run` 메서드를 호출합니다(`OnStart` 메서드가 완료되는 경우).</span><span class="sxs-lookup"><span data-stu-id="56f65-456">The Azure worker role environment calls the `OnStart` method in the `WorkerRole` class when the worker role is getting started, and it calls the `Run` method when the `OnStart` method finishes.</span></span>

<span data-ttu-id="56f65-457">`OnStart` 메서드는 *.cscfg* 파일에서 데이터베이스 연결 문자열을 가져와 Entity Framework DbContext 클래스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-457">The `OnStart` method gets the database connection string from the *.cscfg* file and passes it to the Entity Framework DbContext class.</span></span> <span data-ttu-id="56f65-458">SQLClient 공급자는 기본적으로 사용되므로, 이 공급자를 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-458">The SQLClient provider is used by default, so the provider does not have to be specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="56f65-459">그런 다음, 이 메서드는 저장소 계정에 대한 참조를 가져오고 Blob 컨테이너 및 큐를 만듭니다(없는 경우).</span><span class="sxs-lookup"><span data-stu-id="56f65-459">After that, the method gets a reference to the storage account and creates the blob container and queue if they don't exist.</span></span> <span data-ttu-id="56f65-460">이에 대한 코드는 웹 역할 `Application_Start` 메서드에서 이미 확인한 코드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-460">The code for that is similar to what you already saw in the web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="56f65-461">ContosoAdsWorker - WorkerRole.cs - Run 메서드</span><span class="sxs-lookup"><span data-stu-id="56f65-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="56f65-462">`Run` 메서드는 `OnStart` 메서드가 초기화 작업을 마치면 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-462">The `Run` method is called when the `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="56f65-463">이 메서드는 새 큐 메시지를 찾고 해당 메시지가 도달하면 이를 처리하는 무한 루프를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-463">The method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

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

<span data-ttu-id="56f65-464">각 루프 반복 이후에 큐 메시지를 찾을 수 없는 경우 프로그램은 1초 동안 유휴 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-464">After each iteration of the loop, if no queue message was found, the program sleeps for a second.</span></span> <span data-ttu-id="56f65-465">그러면 작업자 역할이 과도한 CPU 시간 및 저장소 트랜잭션 비용을 발생시키지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-465">This prevents the worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="56f65-466">Microsoft 고객 자문 팀이 말하는 사례에 따르면 개발자가 이를 포함하는 것을 잊고 프로덕션에 배포한 후 휴가를 떠났다가</span><span class="sxs-lookup"><span data-stu-id="56f65-466">The Microsoft Customer Advisory Team tells a story about a  developer who forgot to include this, deployed to production, and left for vacation.</span></span> <span data-ttu-id="56f65-467">돌아온 후에 개발자가 감독하는 데 든 비용이 휴가 비용보다 더 들었다고 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-467">When he got back, his oversight cost more than the vacation.</span></span>

<span data-ttu-id="56f65-468">일부 경우 큐 메시지의 내용으로 인해 처리 오류가 발생하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-468">Sometimes the content of a queue message causes an error in processing.</span></span> <span data-ttu-id="56f65-469">이를 *포이즌 메시지*라고 하며, 단순히 오류를 로깅한 후 루프를 다시 시작하는 경우에는 끊임없이 메시지 처리를 시도할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-469">This is called a *poison message*, and if you just logged an error and restarted the loop, you could endlessly try to process that message.</span></span>  <span data-ttu-id="56f65-470">그러므로 catch 블록은 앱이 현재 메시지를 처리하려고 시도한 횟수를 확인한 후 횟수가 5번이 넘는 경우 큐에서 메시지가 삭제되는 if 문을 포함합니다. 큐 메시지가 발견되는 경우</span><span class="sxs-lookup"><span data-stu-id="56f65-470">Therefore the catch block includes an if statement that checks to see how many times the app has tried to process the current message, and if it has been more than 5 times, the message is deleted from the queue.</span></span>

<span data-ttu-id="56f65-471">큐 메시지가 발견되는 경우 `ProcessQueueMessage`이(가) 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

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

<span data-ttu-id="56f65-472">이 코드는 데이터베이스를 읽어 이미지 URL을 가져오고, 이미지를 미리 보기로 변환하고, 미리 보기를 Blob에 저장하고, 데이터베이스를 미리 보기 Blob URL로 업데이트하고, 큐 메시지를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-472">This code reads the database to get the image URL, converts the image to a thumbnail, saves the thumbnail in a blob, updates the database with the thumbnail blob URL, and deletes the queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="56f65-473">`ConvertImageToThumbnailJPG` 메서드의 코드는 간소화를 위해 System.Drawing 네임스페이스의 클래스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-473">The code in the `ConvertImageToThumbnailJPG` method uses classes in the System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="56f65-474">하지만 이 네임스페이스의 클래스는 Windows Forms에서 사용하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-474">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="56f65-475">Windows 또는 ASP.NET 서비스에서 사용할 수 있도록 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="56f65-476">이미지 처리 옵션에 대한 자세한 내용은 [동적 이미지 생성](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) 및 [이미지 크기 조정 세부 정보](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="56f65-477">문제 해결</span><span class="sxs-lookup"><span data-stu-id="56f65-477">Troubleshooting</span></span>
<span data-ttu-id="56f65-478">이 자습서의 지침을 따르는 동안 무언가가 작동하지 않는 경우 일반적인 오류 및 이를 해결하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-478">In case something doesn't work while you're following the instructions in this tutorial, here are some common errors and how to resolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="56f65-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="56f65-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="56f65-480">Azure에서 응용 프로그램을 실행하거나 Azure 계산 에뮬레이터를 사용하여 로컬에서 실행하면 `RoleEnvironment` 개체가 Azure에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-480">The `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using the Azure compute emulator.</span></span>  <span data-ttu-id="56f65-481">로컬에서 실행할 때 이 오류가 나타나는 경우 ContosoAdsCloudService 프로젝트를 시작 프로젝트로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-481">If you get this error when you're running locally, make sure that you have set the ContosoAdsCloudService project as the startup project.</span></span> <span data-ttu-id="56f65-482">그러면 Azure 계산 에뮬레이터를 사용하여 실행되도록 프로젝트가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-482">This sets up the project to run using the Azure compute emulator.</span></span>

<span data-ttu-id="56f65-483">응용 프로그램이 Azure RoleEnvironment를 사용하는 이유 중 하나는 *.cscfg* 파일에 저장된 연결 문자열 값을 가져오는 것이므로, 이 예외를 일으키는 또 다른 원인은 누락된 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-483">One of the things the application uses the Azure RoleEnvironment for is to get the connection string values that are stored in the *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="56f65-484">ContosoAdsWeb 프로젝트에서 클라우드 및 로컬 구성으로 StorageConnectionString 설정을 만들어야 하며, ContosoAdsWorker 프로젝트에서 두 구성 모두에 대해 두 연결 문자열을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-484">Make sure that you created the StorageConnectionString setting for both Cloud and Local configurations in the ContosoAdsWeb project, and that you created both connection strings for both configurations in the ContosoAdsWorker project.</span></span> <span data-ttu-id="56f65-485">전체 솔루션에서 StorageConnectionString에 대해 **모두 찾기** 로 검색하는 경우 6개 파일에서 9번 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-485">If you do a **Find All** search for StorageConnectionString in the entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-to-port-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="56f65-486">xxx 포트로 재정할 수 없음.</span><span class="sxs-lookup"><span data-stu-id="56f65-486">Cannot override to port xxx.</span></span> <span data-ttu-id="56f65-487">프로토콜 http에 대한 최소 허용 값 8080 미만의 새 포트</span><span class="sxs-lookup"><span data-stu-id="56f65-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="56f65-488">웹 프로젝트에서 사용되는 포트 번호를 변경해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-488">Try changing the port number used by the web project.</span></span> <span data-ttu-id="56f65-489">ContosoAdsWeb 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-489">Right-click the ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="56f65-490">**웹** 탭을 클릭한 다음 **프로젝트 Url** 설정에서 포트 번호를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-490">Click the **Web** tab, and then change the port number in the **Project Url** setting.</span></span>

<span data-ttu-id="56f65-491">문제를 해결할 수 있는 다른 대안은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-491">For another alternative that might resolve the problem, see the following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="56f65-492">로컬 실행 중 다른 오류</span><span class="sxs-lookup"><span data-stu-id="56f65-492">Other errors when running locally</span></span>
<span data-ttu-id="56f65-493">기본적으로 새 클라우드 서비스 프로젝트는 Azure 빠른 계산 에뮬레이터를 사용하여 Azure 환경을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-493">By default new cloud service projects use the Azure compute emulator express to simulate the Azure environment.</span></span> <span data-ttu-id="56f65-494">이는 전체 계산 에뮬레이터의 경량 버전이며, 일부 상황에서 Express 버전이 작동하지 않지만 전체 에뮬레이터는 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-494">This is a lightweight version of the full compute emulator, and under some conditions the full emulator will work when the express version does not.</span></span>  

<span data-ttu-id="56f65-495">전체 에뮬레이터를 사용하도록 프로젝트를 변경하려면 ContosoAdsCloudService 프로젝트를 마우스 오른쪽 단추를 클릭한 다음 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-495">To change the project to use the full emulator, right-click the ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="56f65-496">**속성** 창에서 **웹** 탭을 클릭한 다음 **전체 에뮬레이터 사용** 라디오 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-496">In the **Properties** window click the **Web** tab, and then click the **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="56f65-497">전체 에뮬레이터를 사용하여 응용 프로그램을 실행하려면 관리자 권한으로 Visual Studio를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-497">In order to run the application with the full emulator, you have to open Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56f65-498">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56f65-498">Next steps</span></span>
<span data-ttu-id="56f65-499">Contoso Ads 응용 프로그램은 시작 자습서용으로 의도적으로 단순하게 유지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-499">The Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="56f65-500">예를 들어 이 응용 프로그램은 [종속성 주입](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection)(영문) 또는 [리포지토리 및 작업 단위 패턴](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo)(영문)을 구현하지 않고, [로깅용 인터페이스를 사용](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log)(영문)하지 않으며, 데이터 모델 변경을 관리하는 데 [EF Code First 마이그레이션](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)(영문)을 사용하지 않고, 일시적인 네트워크 오류를 관리하는 데 [EF 연결 복원](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)(영문)을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors, and so forth.</span></span>

<span data-ttu-id="56f65-501">다음은 더 실질적인 코딩 방식을 보여 주는 몇 가지 클라우드 서비스 샘플 응용 프로그램입니다. 복잡성이 낮은 것부터 높은 것 순서로 나열되었습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex to more complex:</span></span>

* <span data-ttu-id="56f65-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31)(영문).</span><span class="sxs-lookup"><span data-stu-id="56f65-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="56f65-503">개념이 Contoso Ads와 비슷하지만, 더 많은 기능과 더 실질적인 코딩 방식을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-503">Similar in concept to Contoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="56f65-504">[테이블, 큐 및 Blob이 포함된 Azure 클라우드 서비스 다중 계층 응용 프로그램](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36)(영문).</span><span class="sxs-lookup"><span data-stu-id="56f65-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="56f65-505">Azure 저장소 테이블 뿐만 아니라 Blob 및 큐를 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="56f65-506">.NET용 Azure SDK의 이전 버전에 기반하여 현재 버전으로 작업하려면 약간 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-506">Based on an older version of the Azure SDK for .NET, will require some modifications to work with the current version.</span></span>
* <span data-ttu-id="56f65-507">[Microsoft Azure의 클라우드 서비스 기본 사항(영문)](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="56f65-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="56f65-508">다양한 모범 사례를 보여 주는 포괄적인 샘플이며 Microsoft 패턴 및 작업 방식 그룹에서 제작했습니다.</span><span class="sxs-lookup"><span data-stu-id="56f65-508">A comprehensive sample demonstrating a wide range of best practices, produced by the Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="56f65-509">클라우드용 개발 관련 일반 정보는 [Azure에서 실제 클라우드 앱 빌드(영문)](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-509">For general information about developing for the cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="56f65-510">Azure 저장소 모범 사례 및 패턴에 대한 비디오 소개는 [Microsoft Azure 저장소 – 새로운 기능, 모범 사례 및 패턴](http://channel9.msdn.com/Events/Build/2014/3-628)(영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-510">For a video introduction to Azure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="56f65-511">자세한 내용은 다음 리소스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56f65-511">For more information, see the following resources:</span></span>

* [<span data-ttu-id="56f65-512">Azure 클라우드 서비스 1 부:</span><span class="sxs-lookup"><span data-stu-id="56f65-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="56f65-513">클라우드 서비스를 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="56f65-513">How to manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="56f65-514">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="56f65-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="56f65-515">클라우드 서비스 공급자 선택 방법</span><span class="sxs-lookup"><span data-stu-id="56f65-515">How to choose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
