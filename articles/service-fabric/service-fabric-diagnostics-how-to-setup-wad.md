---
title: "Azure 진단을 사용하여 로그 수집 | Microsoft Docs"
description: "이 문서는 Azure에서 실행 중인 서비스 패브릭에서 로그를 수집하도록 Azure 진단을 설정하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 9f7e1fa5-6543-4efd-b53f-39510f18df56
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 190a8a393f2e7d74a792db4efa81f94a18b02221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="56407-103">Azure 진단을 사용하여 로그 수집</span><span class="sxs-lookup"><span data-stu-id="56407-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56407-104">Windows</span><span class="sxs-lookup"><span data-stu-id="56407-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="56407-105">Linux</span><span class="sxs-lookup"><span data-stu-id="56407-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="56407-106">Azure 서비스 패브릭 클러스터를 실행할 때 모든 노드의 로그를 중앙 위치에 수집하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-106">When you're running an Azure Service Fabric cluster, it's a good idea to collect the logs from all the nodes in a central location.</span></span> <span data-ttu-id="56407-107">중앙 위치에 로그를 두면 클러스터나 해당 클러스터에서 실행 중인 응용 프로그램 및 서비스의 문제를 분석하고 해결하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-107">Having the logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in the applications and services running in that cluster.</span></span>

<span data-ttu-id="56407-108">로그를 업로드 및 수집하는 방법 중 하나는 로그를 Azure Storage, Azure Application Insights 또는 Azure Event Hubs에 업로드하는 Azure Diagnostics 확장을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56407-108">One way to upload and collect logs is to use the Azure Diagnostics extension, which uploads logs to Azure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="56407-109">로그는 저장소나 Event Hubs에서 크게 직접적인 도움이 되는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="56407-109">The logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="56407-110">하지만 외부 프로세스를 사용하여 저장소의 이벤트를 읽고 [Log Analytics](../log-analytics/log-analytics-service-fabric.md) 또는 기타 로그 구문 분석 솔루션 등의 제품에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-110">But you can use an external process to read the events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="56407-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)에는 포괄적인 로그 검색 및 분석 서비스가 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56407-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="56407-112">Prerequisites</span></span>
<span data-ttu-id="56407-113">이 도구는 이 문서의 일부 작업을 수행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-113">You use these tools to perform some of the operations in this document:</span></span>

* <span data-ttu-id="56407-114">[Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md)(Azure Cloud Services와 관련이 있지만 여러 좋은 정보와 예 제공)</span><span class="sxs-lookup"><span data-stu-id="56407-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related to Azure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="56407-115">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="56407-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="56407-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="56407-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="56407-117">Azure Resource Manager 클라이언트</span><span class="sxs-lookup"><span data-stu-id="56407-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="56407-118">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="56407-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-to-collect"></a><span data-ttu-id="56407-119">수집하려는 로그 원본</span><span class="sxs-lookup"><span data-stu-id="56407-119">Log sources that you might want to collect</span></span>
* <span data-ttu-id="56407-120">**Service Fabric 로그:** 플랫폼에서 표준 ETW(Windows용 이벤트 추적)와 EventSource 채널로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="56407-120">**Service Fabric logs**: Emitted from the platform to standard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="56407-121">로그는 여러 유형 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="56407-122">작업 이벤트: Service Fabric 플랫폼이 수행하는 작업에 대한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="56407-122">Operational events: Logs for operations that the Service Fabric platform performs.</span></span> <span data-ttu-id="56407-123">응용 프로그램 및 서비스 만들기, 노드 상태 변경, 업그레이드 정보 등을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="56407-124">Reliable Actors 프로그래밍 모델 이벤트</span><span class="sxs-lookup"><span data-stu-id="56407-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="56407-125">Reliable Services 프로그래밍 모델 이벤트</span><span class="sxs-lookup"><span data-stu-id="56407-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="56407-126">**응용 프로그램 이벤트:** 서비스 코드에서 발생하며 Visual Studio에서 제공하는 EventSource 도우미 클래스를 사용하여 작성된 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="56407-126">**Application events**: Events emitted from your service's code and written out by using the EventSource helper class provided in the Visual Studio templates.</span></span> <span data-ttu-id="56407-127">응용 프로그램에서 로그를 작성하는 방법에 대한 자세한 내용은 [로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56407-127">For more information on how to write logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-the-diagnostics-extension"></a><span data-ttu-id="56407-128">진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="56407-128">Deploy the Diagnostics extension</span></span>
<span data-ttu-id="56407-129">로그를 수집하는 첫 단계는 서비스 패브릭 클러스터의 각 VM에 진단 확장을 배포하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56407-129">The first step in collecting logs is to deploy the Diagnostics extension on each of the VMs in the Service Fabric cluster.</span></span> <span data-ttu-id="56407-130">진단 확장은 각 VM에서 로그를 수집하여 사용자가 지정하는 저장소 계정에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-130">The Diagnostics extension collects logs on each VM and uploads them to the storage account that you specify.</span></span> <span data-ttu-id="56407-131">단계는 Azure Portal 또는 Azure Resource Manager 사용 여부에 따라 약간 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="56407-131">The steps vary a little based on whether you use the Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="56407-132">또한 배포가 클러스터 생성의 일부인지 아니면 이미 있는 클러스터에 대한 것인지에 따라서도 단계가 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="56407-132">The steps also vary based on whether the deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="56407-133">각 시나리오에 대한 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-133">Let's look at the steps for each scenario.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-through-the-portal"></a><span data-ttu-id="56407-134">포털을 통해 클러스터 만들기의 일환으로 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="56407-134">Deploy the Diagnostics extension as part of cluster creation through the portal</span></span>
<span data-ttu-id="56407-135">클러스터 만들기의 일부로 클러스터의 VM에 진단 확장을 배포하려면 다음 이미지에 표시된 진단 설정 패널을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-135">To deploy the Diagnostics extension to the VMs in the cluster as part of cluster creation, you use the Diagnostics settings panel shown in the following image.</span></span> <span data-ttu-id="56407-136">Reliable Actors 또는 Reliable Services 이벤트 컬렉션을 사용하려면 진단이 기본 설정인 **켜기**로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-136">To enable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set to **On** (the default setting).</span></span> <span data-ttu-id="56407-137">클러스터를 만든 후에는 포털을 사용하여 이러한 설정을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-137">After you create the cluster, you can't change these settings by using the portal.</span></span>

![클러스터를 만들기 위해 포털에서 Azure 진단 설정](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="56407-139">Azure 지원 팀이 사용자의 지원 요청을 처리하려면 지원 로그가 *필요*합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-139">The Azure support team *requires* support logs to help resolve any support requests that you create.</span></span> <span data-ttu-id="56407-140">이러한 로그는 실시간으로 수집되어 리소스 그룹에 만들어진 저장소 계정 중 하나에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-140">These logs are collected in real time and are stored in one of the storage accounts created in the resource group.</span></span> <span data-ttu-id="56407-141">진단 설정은 응용 프로그램 수준 이벤트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-141">The Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="56407-142">이러한 이벤트로는 Azure Storage에 저장될 [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) 이벤트, [Reliable Services](service-fabric-reliable-services-diagnostics.md) 이벤트 및 일부 시스템 수준 Service Fabric 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events to be stored in Azure Storage.</span></span>

<span data-ttu-id="56407-143">[Elasticsearch](https://www.elastic.co/guide/index.html) 등의 제품이나 사용자 고유의 프로세스는 저장소 계정에서 이벤트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get the events from the storage account.</span></span> <span data-ttu-id="56407-144">현재 테이블로 전송되는 이벤트를 필터링하거나 영구 제거할 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-144">There is currently no way to filter or groom the events that are sent to the table.</span></span> <span data-ttu-id="56407-145">테이블에서 이벤트를 제거하는 프로세스를 구현하지 않으면 테이블이 계속 커집니다.</span><span class="sxs-lookup"><span data-stu-id="56407-145">If you don't implement a process to remove events from the table, the table will continue to grow.</span></span>

<span data-ttu-id="56407-146">포털을 사용하여 클러스터를 만드는 경우 클러스터를 만들기 위해 **확인을 클릭하기 전에** 템플릿을 다운로드하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-146">When you're creating a cluster by using the portal, we highly recommend that you download the template **before you click OK** to create the cluster.</span></span> <span data-ttu-id="56407-147">자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 Service Fabric 클러스터 설정](service-fabric-cluster-creation-via-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56407-147">For details, refer to [Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="56407-148">일부는 포털을 사용하여 변경할 수 없으므로 나중에 변경하려면 템플릿이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-148">You'll need the template to make changes later, because you can't make some changes by using the portal.</span></span>

<span data-ttu-id="56407-149">다음 단계에 따라 포털에서 템플릿을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-149">You can export templates from the portal by using the following steps.</span></span> <span data-ttu-id="56407-150">그러나 이러한 템플릿은 필요한 정보를 누락된 null 값이 포함될 수 있으므로 사용하기 더 어려울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-150">However, these templates can be more difficult to use because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="56407-151">리소스 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56407-151">Open your resource group.</span></span>
2. <span data-ttu-id="56407-152">**설정**을 선택하여 설정 패널을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-152">Select **Settings** to display the settings panel.</span></span>
3. <span data-ttu-id="56407-153">**배포**를 선택하여 배포 기록 패널을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-153">Select **Deployments** to display the deployment history panel.</span></span>
4. <span data-ttu-id="56407-154">배포 세부 정보를 표시할 배포를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-154">Select a deployment to display the details of the deployment.</span></span>
5. <span data-ttu-id="56407-155">**템플릿 내보내기**를 선택하여 템플릿은 패널을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-155">Select **Export Template** to display the template panel.</span></span>
6. <span data-ttu-id="56407-156">**파일에 저장**을 선택하여 템플릿, 매개 변수 및 PowerShell 파일을 포함하는 .zip 파일을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="56407-156">Select **Save to file** to export a .zip file that contains the template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="56407-157">파일을 내보낸 후 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-157">After you export the files, you need to make a modification.</span></span> <span data-ttu-id="56407-158">parameters.json 파일을 편집하고 **adminPassword** 요소를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-158">Edit the parameters.json file and remove the **adminPassword** element.</span></span> <span data-ttu-id="56407-159">배포 스크립트가 실행될 때 암호를 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-159">This will cause a prompt for the password when the deployment script is run.</span></span> <span data-ttu-id="56407-160">배포 스크립트를 실행할 때 null 매개 변수 값을 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-160">When you're running the deployment script, you might have to fix null parameter values.</span></span>

<span data-ttu-id="56407-161">다운로드한 템플릿을 사용하여 구성을 업데이트하려면:</span><span class="sxs-lookup"><span data-stu-id="56407-161">To use the downloaded template to update a configuration:</span></span>

1. <span data-ttu-id="56407-162">로컬 컴퓨터의 폴더에 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="56407-162">Extract the contents to a folder on your local computer.</span></span>
2. <span data-ttu-id="56407-163">새 구성을 반영하도록 콘텐츠를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-163">Modify the contents to reflect the new configuration.</span></span>
3. <span data-ttu-id="56407-164">PowerShell을 시작하고 압축을 푼 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-164">Start PowerShell and change to the folder where you extracted the content.</span></span>
4. <span data-ttu-id="56407-165">**deploy.ps1** 을 실행하고 구독 ID, 리소스 그룹 이름(같은 이름을 사용하여 구성 업데이트) 및 고유한 배포 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-165">Run **deploy.ps1** and fill in the subscription ID, the resource group name (use the same name to update the configuration), and a unique deployment name.</span></span>

### <a name="deploy-the-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="56407-166">Azure 리소스 관리자를 사용하여 클러스터 만들기의 일환으로 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="56407-166">Deploy the Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="56407-167">리소스 관리자를 사용하여 클러스터를 만들려면 클러스터를 만들기 전에 진단 구성 JSON을 전체 클러스터 Resource Manager 템플릿에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-167">To create a cluster by using Resource Manager, you need to add the Diagnostics configuration JSON to the full cluster Resource Manager template before you create the cluster.</span></span> <span data-ttu-id="56407-168">Resource Manager 템플릿 샘플의 일부로 진단 구성이 추가된 샘플 5VM 클러스터 Resource Manager 템플릿이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added to it as part of our Resource Manager template samples.</span></span> <span data-ttu-id="56407-169">Azure 샘플 갤러리의 [진단 Resource Manager 템플릿 샘플이 포함된 5노드 클러스터](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)에서 샘플을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-169">You can see it at this location in the Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="56407-170">Resource Manager 템플릿에서 진단 설정을 표시하려면 azuredeploy.json 파일을 열고 **IaaSDiagnostics**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-170">To see the Diagnostics setting in the Resource Manager template, open the azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="56407-171">이 템플릿을 사용하여 클러스터를 만들려면 이전 링크에 제공된 **Azure에 배포** 버튼을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-171">To create a cluster by using this template, select the **Deploy to Azure** button available at the previous link.</span></span>

<span data-ttu-id="56407-172">또는 리소스 관리자 샘플을 다운로드하여 변경한 후 Azure PowerShell 창에서 `New-AzureRmResourceGroupDeployment` 명령을 사용하여 수정된 템플릿으로 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-172">Alternatively, you can download the Resource Manager sample, make changes to it, and create a cluster with the modified template by using the `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="56407-173">명령에 전달할 매개 변수는 다음 코드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56407-173">See the following code for the parameters that you pass in to the command.</span></span> <span data-ttu-id="56407-174">PowerShell을 사용하여 리소스 그룹을 배포하는 방법에 대한 자세한 내용은 [Azure Resource Manager 템플릿을 사용하여 리소스 그룹 배포](../azure-resource-manager/resource-group-template-deploy.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56407-174">For detailed information on how to deploy a resource group by using PowerShell, see the article [Deploy a resource group with the Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-the-diagnostics-extension-to-an-existing-cluster"></a><span data-ttu-id="56407-175">기존 클러스터에 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="56407-175">Deploy the Diagnostics extension to an existing cluster</span></span>
<span data-ttu-id="56407-176">진단이 배포되지 않은 기존 클러스터가 있거나 기존 구성을 수정하려는 경우 기존 클러스터를 추가하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want to modify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="56407-177">기존 클러스터를 만드는 데 사용되는 Resource Manager 템플릿을 수정하거나 앞의 설명대로 포털에서 템플릿을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-177">Modify the Resource Manager template that's used to create the existing cluster or download the template from the portal as described earlier.</span></span> <span data-ttu-id="56407-178">다음 작업을 수행하여 template.json 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-178">Modify the template.json file by performing the following tasks.</span></span>

<span data-ttu-id="56407-179">리소스 섹션에 추가하여 새 저장소 리소스를 템플릿에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-179">Add a new storage resource to the template by adding to the resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="56407-180">저장소 계정 정의 바로 뒤 `supportLogStorageAccountName`과 `vmNodeType0Name` 사이의 매개 변수 섹션에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-180">Next, add to the parameters section just after the storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="56407-181">자리 표시자 텍스트 *storage account name goes here*를 저장소 계정의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="56407-181">Replace the placeholder text *storage account name goes here* with the name of the storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for the application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for the storage account that contains application diagnostics data from the cluster"
      }
    },
```
<span data-ttu-id="56407-182">그런 다음 확장 배열 내에 다음 코드를 추가하여 template.json의 `VirtualMachineProfile` 섹션을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-182">Then, update the `VirtualMachineProfile` section of the template.json file by adding the following code within the extensions array.</span></span> <span data-ttu-id="56407-183">삽입되는 위치에 따라 시작 부분 또는 끝 부분에 쉼표를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-183">Be sure to add a comma at the beginning or the end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="56407-184">template.json 파일을 설명대로 수정한 후에는 Resource Manager 템플릿을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-184">After you modify the template.json file as described, republish the Resource Manager template.</span></span> <span data-ttu-id="56407-185">템플릿을 내보낸 후 deploy.ps1 파일을 실행하면 템플릿이 다시 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-185">If the template was exported, running the deploy.ps1 file republishes the template.</span></span> <span data-ttu-id="56407-186">배포 후에는 **ProvisioningState**가 **성공**했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-to-collect-health-and-load-events"></a><span data-ttu-id="56407-187">진단을 컬렉션 상태 및 부하 이벤트에 업데이트</span><span class="sxs-lookup"><span data-stu-id="56407-187">Update diagnostics to collect health and load events</span></span>

<span data-ttu-id="56407-188">Service Fabric 5.4 버전부터 상태 및 부하 메트릭 이벤트를 컬렉션에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56407-188">Starting with the 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="56407-189">이러한 이벤트는 시스템이나 코드에서 [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) 또는 [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx) 등의 상태 또는 부하 보고 API를 사용하여 시스템 또는 코드에서 생성한 이벤트를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-189">These events reflect events generated by the system or your code by using the health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="56407-190">이를 통해 시간 경과에 따른 시스템 상태의 집계 및 확인과 상태 또는 부하 이벤트 기반의 경고가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="56407-191">Visual Studio의 Diagnostic Event Viewer에서 이 이벤트를 보려면 ETW 공급자 목록에 "Microsoft-ServiceFabric:4:0x4000000000000008"을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-191">To view these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" to the list of ETW providers.</span></span>

<span data-ttu-id="56407-192">이벤트를 수집하려면 Resource Manager 템플릿을 수정하여 다음을 포함하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-192">To collect the events, modify the resource manager template to include</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="update-diagnostics-to-collect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="56407-193">새 EventSource 채널에서 로그를 수집 및 업로드하도록 진단 업데이트</span><span class="sxs-lookup"><span data-stu-id="56407-193">Update Diagnostics to collect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="56407-194">배포하려는 새 응용 프로그램을 나타내는 새 EventSource 채널에서 로그를 수집하도록 진단을 업데이트하려면 기존 클러스터에 대한 진단 설정을 설명하는 [이전 섹션](#deploywadarm)과 동일한 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-194">To update Diagnostics to collect logs from new EventSource channels that represent a new application that you're about to deploy, perform the same steps as in the [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="56407-195">새 EventSource 채널의 항목을 추가하도록 template.json 파일의 `EtwEventSourceProviderConfiguration` 섹션을 업데이트한 후 `New-AzureRmResourceGroupDeployment` PowerShell 명령을 사용하여 구성 업데이트를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-195">Update the `EtwEventSourceProviderConfiguration` section in the template.json file to add entries for the new EventSource channels before you apply the configuration update by using the `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="56407-196">이벤트 원본의 이름은 ServiceEventSource.cs 파일을 생성한 Visual Studio에서 코드의 일부로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="56407-196">The name of the event source is defined as part of your code in the Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="56407-197">예를 들어 이벤트 원본의 이름을 Eventsource라고 지정한 경우 My-Eventsource의 이벤트를 MyDestinationTableName이라는 테이블에 배치하는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-197">For example, if your event source is named My-Eventsource, add the following code to place the events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="56407-198">성능 카운터 또는 이벤트 로그를 수집하려면 [Azure Resource Manager 템플릿을 사용하여 모니터링 및 진단이 포함된 Windows 가상 컴퓨터 만들기](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에 제공된 예제를 사용하여 Resource Manager 템플릿을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-198">To collect performance counters or event logs, modify the Resource Manager template by using the examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="56407-199">그런 다음 Resource Manager 템플릿을 다시 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-199">Then, republish the Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56407-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56407-200">Next steps</span></span>
<span data-ttu-id="56407-201">문제를 해결하는 동안 조사해야 하는 이벤트에 대한 자세한 내용을 확인하려면 [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) 및 [Reliable Services](service-fabric-reliable-services-diagnostics.md)가 내보낸 진단 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="56407-201">To understand in more detail what events you should look for while troubleshooting issues, see the diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="56407-202">관련 문서</span><span class="sxs-lookup"><span data-stu-id="56407-202">Related articles</span></span>
* [<span data-ttu-id="56407-203">진단 확장을 사용하여 성능 카운터 또는 로그를 수집하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="56407-203">Learn how to collect performance counters or logs by using the Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="56407-204">Log Analytics의 Service Fabric 솔루션</span><span class="sxs-lookup"><span data-stu-id="56407-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

