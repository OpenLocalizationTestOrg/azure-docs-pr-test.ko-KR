---
title: "Azure SDK for .NET 2.8 릴리스 정보"
description: "Azure SDK for .NET 2.8 릴리스 정보"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 0b9f55d69c824e86245738a082f95fc529583f58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a><span data-ttu-id="022c7-103">Azure SDK for .NET 2.8, 2.8.1, 2.8.2</span><span class="sxs-lookup"><span data-stu-id="022c7-103">Azure SDK for .NET 2.8, 2.8.1 and 2.8.2</span></span>
## <a name="overview"></a><span data-ttu-id="022c7-104">개요</span><span class="sxs-lookup"><span data-stu-id="022c7-104">Overview</span></span>
<span data-ttu-id="022c7-105">이 문서에는 Azure SDK for .NET 2.8, 2.8.1, 2.8.2 릴리스에 대한 알려진 문제와 주요 변경 내용을 포함하는 릴리스 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-105">This article contains the release notes (that includes known issues and breaking changes) for the Azure SDK for .NET 2.8, 2.8.1 and 2.8.2 releases.</span></span> 

<span data-ttu-id="022c7-106">이 릴리스의 새로운 기능 및 업데이트에 대한 전체 목록은 [Visual Studio 2013 및 Visual Studio 2015용 Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) 알림을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="022c7-106">For complete list of new features and updates made in this release, see the [Azure SDK 2.8 for Visual Studio 2013 and Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) announcement.</span></span> 

## <a name="azure-sdk-for-net-28"></a><span data-ttu-id="022c7-107">Azure SDK for .NET 2.8</span><span class="sxs-lookup"><span data-stu-id="022c7-107">Azure SDK for .NET 2.8</span></span>
### <a name="download-azure-sdk-for-net-28"></a><span data-ttu-id="022c7-108">Azure SDK for .NET 2.8 다운로드</span><span class="sxs-lookup"><span data-stu-id="022c7-108">Download Azure SDK for .NET 2.8</span></span>
[<span data-ttu-id="022c7-109">Visual Studio 2015용 Azure SDK for .NET 2.8</span><span class="sxs-lookup"><span data-stu-id="022c7-109">Azure SDK for .NET 2.8 for Visual Studio 2015</span></span>](http://go.microsoft.com/fwlink/?LinkId=699285) 

[<span data-ttu-id="022c7-110">Visual Studio 2013용 Azure SDK for .NET 2.8</span><span class="sxs-lookup"><span data-stu-id="022c7-110">Azure SDK for .NET 2.8 for Visual Studio 2013</span></span>](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a><span data-ttu-id="022c7-111">.NET 4.5.2 지원</span><span class="sxs-lookup"><span data-stu-id="022c7-111">.NET 4.5.2 support</span></span>
#### <a name="known-issues"></a><span data-ttu-id="022c7-112">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="022c7-112">Known issues</span></span>
<span data-ttu-id="022c7-113">Azure .NET SDK 2.8을 사용하여 .NET 4.5.2 클라우드 서비스 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-113">Azure .NET SDK 2.8 allows you to create .NET 4.5.2 Cloud Service packages.</span></span> <span data-ttu-id="022c7-114">그러나 .NET 4.5.2 프레임워크는 기본 게스트 OS 이미지에 설치되지 않습니다(게스트 OS 2016년 1월 버전까지).</span><span class="sxs-lookup"><span data-stu-id="022c7-114">However .NET 4.5.2 framework will not be installed on the default Guest OS images until January 2016 Guest OS release.</span></span> <span data-ttu-id="022c7-115">그전에는 .NET 4.5.2 프레임워크를 별도 게스트 OS 릴리스 버전(2015년 11월-02)을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-115">Before that, .NET 4.5.2 framework will be available through a separate Guest OS release version – November 2015-02.</span></span> <span data-ttu-id="022c7-116">이미지가 릴리스되는 시기를 추적하려면 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](../cloud-services/cloud-services-guestos-update-matrix.md) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="022c7-116">See the [Azure Guest OS Releases and SDK Compatibility Matrix](../cloud-services/cloud-services-guestos-update-matrix.md) page to track when the image will be released.</span></span>  <span data-ttu-id="022c7-117">2015년 11월-02 이미지가 릴리스되면 클라우드 서비스 구성 파일(.cscfg)을 업데이트하여 해당 이미지를 사용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-117">Once the November 2015-02 image is released you can choose to use that image by updating your Cloud Service configuration file (.cscfg) file.</span></span> <span data-ttu-id="022c7-118">서비스 구성 파일에서 ServiceConfiguration 요소의 osVersion 특성을 문자열 "WA-GUEST-OS-4.26_201511-02"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-118">In the service configuration file set the osVersion attribute of the ServiceConfiguration element to the string "WA-GUEST-OS-4.26_201511-02".</span></span> <span data-ttu-id="022c7-119">이 이미지를 사용하도록 선택한 경우 더 이상 게스트 OS에 대한 자동 업데이트를 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-119">If you choose to opt in to use this image then you will no longer get automatic updates to the Guest OS.</span></span> <span data-ttu-id="022c7-120">자동 업데이트를 받으려면 osVersion이 “*”로 설정되어 있어야 하며 .NET 4.5.2는 2016년 1월 자동 업데이트를 통해서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-120">To get the automatic updates the osVersion must be set to “*” and .NET 4.5.2 will only be available through automatic updates in January 2016.</span></span>

### <a name="azure-data-factory"></a><span data-ttu-id="022c7-121">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="022c7-121">Azure Data Factory</span></span>
#### <a name="known-issues"></a><span data-ttu-id="022c7-122">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="022c7-122">Known issues</span></span>
<span data-ttu-id="022c7-123">샘플 데이터를 포함하는 **데이터 팩터리 템플릿** 프로젝트를 만드는 동안 컴퓨터에 설치된 Azure PowerShell 버전이 0.9.8 이후이면 Azure PowerShell 스크립트가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-123">During a **Data Factory Template** project creation involving sample data, azure power shell script may fail if azure power shell version installed on the machine is after 0.9.8.</span></span>

<span data-ttu-id="022c7-124">이 유형의 프로젝트를 성공적으로 만들려면 [Azure PowerShell 버전 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi)을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-124">In order to successfully create this type of project, you must install [azure power shell version  0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).</span></span>

### <a name="azure-resource-manager-tools"></a><span data-ttu-id="022c7-125">Azure 리소스 관리자 도구</span><span class="sxs-lookup"><span data-stu-id="022c7-125">Azure Resource Manager Tools</span></span>
#### <a name="breaking-changes"></a><span data-ttu-id="022c7-126">주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="022c7-126">Breaking changes</span></span>
<span data-ttu-id="022c7-127">Azure 리소스 그룹 프로젝트에서 제공한 PowerShell 스크립트가 새 Azure PowerShell cmdlet 버전 1.0을 사용하여 작업하도록 이 릴리스에서 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-127">The PowerShell script provided by the Azure Resource Group project has been updated in this release to work with the new Azure PowerShell cmdlets version 1.0.</span></span>  <span data-ttu-id="022c7-128">이 새로운 스크립트는 SDK 2.8 이전 버전을 사용하는 경우 Visual Studio에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-128">This new script will not work from with Visual Studio when using a version of the SDK prior to 2.8.</span></span>  

<span data-ttu-id="022c7-129">이전 버전의 SDK에서 만든 프로젝트의 스크립트는 SDK 2.8을 사용하면 Visual Studio 내에서 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-129">Scripts from projects created in earlier versions of the SDK will not run from within Visual Studio when using the 2.8 SDK.</span></span>  <span data-ttu-id="022c7-130">모든 스크립트는 Azure PowerShell cmdlet의 적절한 버전을 사용하여 Visual Studio 외부에서 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-130">All scripts will continue to work outside of Visual Studio with the appropriate version of the Azure PowerShell cmdlets.</span></span>  

<span data-ttu-id="022c7-131">SDK 2.8을 사용하려면 Azure PowerShell cmdlet 버전 1.0이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-131">The 2.8 SDK requires version 1.0 of the Azure PowerShell cmdlets.</span></span>  <span data-ttu-id="022c7-132">다른 모든 버전의 SDK를 사용하려면 Azure PowerShell cmdlet 버전 0.9.8이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-132">All other versions of the SDK require version 0.9.8 of the Azure PowerShell cmdlets.</span></span>  <span data-ttu-id="022c7-133">자세한 내용은 [이 블로그](http://go.microsoft.com/fwlink/?LinkID=623011)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="022c7-133">For more information see [this](http://go.microsoft.com/fwlink/?LinkID=623011) blog.</span></span>

### <a name="web-tools-extensions"></a><span data-ttu-id="022c7-134">웹 도구 확장</span><span class="sxs-lookup"><span data-stu-id="022c7-134">Web Tools Extensions</span></span>
#### <a name="known-issues"></a><span data-ttu-id="022c7-135">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="022c7-135">Known issues</span></span>
<span data-ttu-id="022c7-136">다음과 같이 알려진 문제는 다음 릴리스에서 해결된 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-136">The following known issues will be addressed in the following release.</span></span>

* <span data-ttu-id="022c7-137">비프로덕션 환경(예: Azure China 또는 Azure 스택 고객)에서는 앱 서비스 관련 클라우드 및 서버 탐색기 제스처가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-137">App Service related Cloud and Server Explorer gesture for non-production environments (like Azure China or Azure Stack customers) do not work.</span></span> <span data-ttu-id="022c7-138">이러한 영향을 받는 지역의 고객은 Azure 포털에서 게시 프로필을 다운로드하면 게시 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-138">For customers in these impacted areas, downloading the publish profile from the Azure portal will enable publishing ability.</span></span> <span data-ttu-id="022c7-139">향후 릴리스에서 Azure China 및 스택 고객에 대한 "디버거 연결" 및 "스트리밍 로그 보기"와 같은 제스처가 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-139">A future release will repair gestures such as “Attach Debugger” and “View Streaming Logs” for Azure China and Stack customers.</span></span> 
* <span data-ttu-id="022c7-140">배포하려는 App Insights 인스턴스가 미국 동부 이외의 지역에 있는 경우 앱 서비스를 만드는 동안 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-140">Customers may see errors during App Service creation when the App Insights instance to which they are deploying is in a region other than East US.</span></span> <span data-ttu-id="022c7-141">이러한 시나리오에서는 포털에서 앱 서비스를 만들고 게시 프로필을 다운로드하면 게시 시나리오를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-141">In these scenarios, creating an App Service in the portal and downloading the publish profile will enable publishing scenarios.</span></span> 

### <a name="azure-hdinsight-tools"></a><span data-ttu-id="022c7-142">Azure HDInsight 도구</span><span class="sxs-lookup"><span data-stu-id="022c7-142">Azure HDInsight Tools</span></span>
#### <a name="new-updates"></a><span data-ttu-id="022c7-143">새 업데이트</span><span class="sxs-lookup"><span data-stu-id="022c7-143">New updates</span></span>
* <span data-ttu-id="022c7-144">거의 오버헤드 없이 HiveServer2를 통해 클러스터에서 Hive 쿼리를 실행하고 작업 기록을 실시간으로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-144">You can execute your Hive query in the cluster via HiveServer2 with almost no overhead and see the job logs in real-time.</span></span>
* <span data-ttu-id="022c7-145">새 Hive 작업 실행 보기를 사용하여 작업을 자세히 살펴볼 수 있으며 자세한 정보를 찾아 잠재적인 문제를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-145">Using the new Hive Task Execution View you can dig into your job deeper, find more details, and identify potential issues.</span></span>

<span data-ttu-id="022c7-146">자세한 내용은 [Visual Studio 2013 및 Visual Studio 2015용 Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="022c7-146">For information, see [Azure SDK 2.8 for Visual Studio 2013 and Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span> 

## <a name="azure-sdk-for-net-281"></a><span data-ttu-id="022c7-147">Azure SDK for .NET 2.8.1</span><span class="sxs-lookup"><span data-stu-id="022c7-147">Azure SDK for .NET 2.8.1</span></span>
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="022c7-148">Visual Studio 2013 및 Visual Studio 2015에 대해 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="022c7-148">Known Issues for Visual Studio 2013 and Visual Studio 2015</span></span>
1. <span data-ttu-id="022c7-149">트리거된 WebJob이 슬롯에 게시되면 오류가 표시되면서 예약이 설정되지 않지만 WebJob을 Azure에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-149">Triggered WebJob publishes to slots will show and error and won’t set a schedule, but it will push the WebJob to Azure.</span></span> <span data-ttu-id="022c7-150">예약된 작업이 필요한 고객은 Azure 포털을 사용하여 WebJob에 대해 예약을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-150">Customers who are in need of a Scheduled job can then use the Azure Portal to set up the schedule for the WebJob.</span></span> 
2. <span data-ttu-id="022c7-151">Python 고객에게 디버거 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-151">Python customers may experience debugger issues.</span></span> <span data-ttu-id="022c7-152">서비스 팀은 이 문제에 대한 픽스를 내놓고 있지만 고객이 영향을 받는 경우 포럼 또는 공지 블로그나 릴리스 정보 의견 섹션을 통해 Microsoft에 알려 주세요.</span><span class="sxs-lookup"><span data-stu-id="022c7-152">Service team is rolling out a fix for this but if customers are affected, please let Microsoft know in the forums or on the announcement blog or release notes comments section.</span></span> 
3. <span data-ttu-id="022c7-153">특정 지역(예: 인도 남부)의 고객에게 앱 서비스 프로비저닝 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-153">Customers in certain regions (such as South India) will experience App Service provisioning errors.</span></span> <span data-ttu-id="022c7-154">이는 포털과 일치하며 이 문제가 발생하는 고객은 Azure 포털을 사용하여 이러한 지역에 게시하기 위해 액세스를 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-154">This is consistent with the portal, and customers who experience this issue can use the Azure portal to request access to publish to these geo-regions.</span></span> <span data-ttu-id="022c7-155">Azure 포털을 사용하여 이러한 지역에 대한 액세스를 요청하면 프로비저닝이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-155">Once they request access to these regions using the Azure portal provisioning should work.</span></span> 

## <a name="azure-sdk-for-net-282"></a><span data-ttu-id="022c7-156">Azure SDK for .NET 2.8.2</span><span class="sxs-lookup"><span data-stu-id="022c7-156">Azure SDK for .NET 2.8.2</span></span>
<span data-ttu-id="022c7-157">2.8.2 도구를 설치한 후 고객에게 다음과 같은 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-157">Following the installation of the 2.8.2 tools, customers may experience the following issue.</span></span>         

* <span data-ttu-id="022c7-158">Internet Explorer를 설치하지 않고 Windows 10을 사용하는 경우 "Internet Explorer를 찾을 수 없습니다"라는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-158">If you are using Windows 10 and have not installed Internet Explorer, you may get an "Internet Explorer could not be found" error.</span></span>
  <span data-ttu-id="022c7-159">이 문제를 해결하려면 Windows 구성 요소 추가/제거 대화 상자를 사용하여 Internet Explorer를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-159">To resolve the issue, install Internet Explorer using the Add/Remove Windows Components dialog.</span></span>

<span data-ttu-id="022c7-160">이러한 문제를 확인하면 웃는 얼굴 보내기 기능을 사용하여 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="022c7-160">If you observe this issue, use the Send-a-smile feature to report it.</span></span>

<span data-ttu-id="022c7-161">자세한 내용은 [이 게시물](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="022c7-161">For more information, see [this](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) post.</span></span>

## <a name="other-updates"></a><span data-ttu-id="022c7-162">다른 업데이트</span><span class="sxs-lookup"><span data-stu-id="022c7-162">Other updates</span></span>
<span data-ttu-id="022c7-163">다른 업데이트는 [Azure SDK 2.8 발표 게시물](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="022c7-163">For other updates, see [Azure SDK 2.8 announcement post](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="also-see"></a><span data-ttu-id="022c7-164">참고 항목</span><span class="sxs-lookup"><span data-stu-id="022c7-164">Also see</span></span>
[<span data-ttu-id="022c7-165">Azure SDK 2.8 발표 게시물</span><span class="sxs-lookup"><span data-stu-id="022c7-165">Azure SDK 2.8 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[<span data-ttu-id="022c7-166">.NET 및 API용 Azure SDK에 대한 지원 및 사용 중지 정보</span><span class="sxs-lookup"><span data-stu-id="022c7-166">Support and Retirement Information for the Azure SDK for .NET and APIs</span></span>](https://msdn.microsoft.com/library/azure/dn479282.aspx)

