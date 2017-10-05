---
title: "Azure Portal을 사용하여 Log Analytics로 Service Fabric 응용 프로그램 평가 | Microsoft Docs"
description: "Azure Portal에서 Log Analytics의 Service Fabric 솔루션을 사용하여 Service Fabric 응용 프로그램, 마이크로 서비스, 노드 및 클러스터의 위험과 상태를 평가할 수 있습니다."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 8c564c0dcbb2f9be286917b2f4d8a40da5406fae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-the-azure-portal"></a><span data-ttu-id="525d6-103">Azure Portal에서 Service Fabric 응용 프로그램 및 마이크로 서비스 평가</span><span class="sxs-lookup"><span data-stu-id="525d6-103">Assess Service Fabric applications and micro-services with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="525d6-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="525d6-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="525d6-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="525d6-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Service Fabric 기호](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="525d6-107">이 문서에서는 Log Analytics에서 Service Fabric 솔루션을 사용하여 Service Fabric 클러스터 간의 문제를 파악 및 해결하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="525d6-108">Service Fabric 솔루션은 Azure WAD 테이블에서 이 데이터를 수집하여 Service Fabric VM에서 Azure 진단 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-108">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="525d6-109">그러면 Log Analytics에서는 **Reliable Service 이벤트**, **행위자 이벤트**, **작업 이벤트**, **사용자 지정 ETW 이벤트**를 포함한 Service Fabric 프레임워크 이벤트를 읽어옵니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="525d6-110">솔루션 대시보드를 통해 Service Fabric 환경에서 주목할 만한 문제와 관련 이벤트를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-110">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="525d6-111">솔루션을 시작하려면 Service Fabric 클러스터를 Log Analytics 작업 영역에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-111">To get started with the solution, you need to connect your Service Fabric cluster to a Log Analytics workspace.</span></span> <span data-ttu-id="525d6-112">세 가지 시나리오를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-112">Here are three scenarios to consider:</span></span>

1. <span data-ttu-id="525d6-113">Service Fabric 클러스터를 배포하지 않은 경우 ***Log Analytics 작업 영역에 연결된 Service Fabric 클러스터 배포***의 단계에 따라 새 클러스터를 배포하고 Log Analytics에 보고하도록 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-113">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span></span>
2. <span data-ttu-id="525d6-114">Service Fabric 클러스터의 보안과 같은 다른 OMS 솔루션을 사용하기 위해 호스트에서 성능 카운터를 수집해야 할 경우 ***VM 확장이 설치된 Log Analytics 작업 영역에 연결된 Service Fabric 클러스터 배포***의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-114">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="525d6-115">Service Fabric 클러스터를 이미 배포했고 Log Analytics에 연결하려는 경우 ***기존 저장소 계정을 Log Analytics에 추가***의 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-115">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace"></a><span data-ttu-id="525d6-116">Log Analytics 작업 영역에 연결된 Service Fabric 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-116">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span></span>
<span data-ttu-id="525d6-117">이 템플릿은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-117">This template does the following:</span></span>

1. <span data-ttu-id="525d6-118">Log Analytics 작업 영역에 이미 연결된 Azure Service Fabric 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-118">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="525d6-119">템플릿을 배포하는 동안 새 작업 영역을 만들 수 있는 옵션이 제공되거나 기존의 Log Analytics 작업 영역의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-119">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="525d6-120">진단 저장소 계정을 Log Analytics 작업 영역에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-120">Adds the diagnostic storage account to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="525d6-121">Log Analytics 작업 영역에서 Service Fabric 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-121">Enables the Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="525d6-122">[![Azure에 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="525d6-122">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="525d6-123">위의 배포 단추를 선택하면 편집할 매개 변수가 있는 Azure Portal로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-123">Once you select the deploy button above, the Azure portal opens with parameters for you to edit.</span></span> <span data-ttu-id="525d6-124">새 Log Analytics 작업 영역 이름을 입력하는 경우 새 리소스 그룹을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-124">Be sure to create a new resource group if you input a new Log Analytics workspace name:</span></span>

![서비스 패브릭](./media/log-analytics-service-fabric/2.png)

![서비스 패브릭](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="525d6-127">약관에 동의하고 **만들기**를 클릭하여 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-127">Accept the legal terms and click **Create** to start the deployment.</span></span> <span data-ttu-id="525d6-128">배포가 완료되면 새 작업 영역 및 클러스터가 생성되고 WADServiceFabric*Event, WADWindowsEventLogs 및 WADETWEvent 테이블이 추가되는 것이 보입니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-128">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![서비스 패브릭](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="525d6-130">VM 확장이 설치된 Log Analytics 작업 영역에 연결된 Service Fabric 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-130">Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="525d6-131">이 템플릿은 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-131">This template does the following:</span></span>

1. <span data-ttu-id="525d6-132">Log Analytics 작업 영역에 이미 연결된 Azure Service Fabric 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-132">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="525d6-133">새 작업 영역을 만들거나 기존 작업 영역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="525d6-134">진단 저장소 계정을 Log Analytics 작업 영역에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-134">Adds the diagnostic storage accounts to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="525d6-135">Log Analytics 작업 영역에서 Service Fabric 솔루션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-135">Enables the Service Fabric solution in the Log Analytics workspace.</span></span>
4. <span data-ttu-id="525d6-136">Service Fabric 클러스터의 각 가상 컴퓨터 확장 집합에 MMA 에이전트 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-136">Installs the MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="525d6-137">MMA 에이전트가 설치되면 노드에 대한 성능 메트릭을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-137">With the MMA agent installed, you are able to view performance metrics about your nodes.</span></span>

<span data-ttu-id="525d6-138">[![Azure에 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="525d6-138">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="525d6-139">위와 동일한 단계에 따라 필요한 매개 변수를 입력하고 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-139">Following the same steps above, input the necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="525d6-140">다시 한 번 새 작업 영역, 클러스터 및 생성된 모든 WAD 테이블이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-140">Once again you should see the new workspace, cluster and WAD tables all created:</span></span>

![서비스 패브릭](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="525d6-142">성능 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="525d6-142">Viewing Performance Data</span></span>

<span data-ttu-id="525d6-143">노드에서 성능 데이터를 보려면:</span><span class="sxs-lookup"><span data-stu-id="525d6-143">To view Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="525d6-144">Azure 포털에서 Log Analytics 작업 영역을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-144">Launch the Log Analytics workspace from the Azure portal.</span></span>
  <span data-ttu-id="525d6-145">![서비스 패브릭](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="525d6-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="525d6-146">왼쪽 창의 설정으로 이동하고 데이터 >> Windows 성능 카운터 >> "Add the selected performance counters(선택한 성능 카운터 추가)": ![Service Fabric](./media/log-analytics-service-fabric/7.png)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-146">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="525d6-147">로그 검색에서 다음 쿼리를 사용하여 노드에 대한 주요 메트릭을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-147">In Log Search, use the following queries to delve into key metrics about your nodes:</span></span>

    <span data-ttu-id="525d6-148">a.</span><span class="sxs-lookup"><span data-stu-id="525d6-148">a.</span></span> <span data-ttu-id="525d6-149">최근 1시간 동안 모든 노드에 대한 평균 CPU 사용률을 비교하여 어떤 노드에 문제가 있으며 노드에 급증이 나타나는 시간 간격을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-149">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="525d6-151">b.</span><span class="sxs-lookup"><span data-stu-id="525d6-151">b.</span></span> <span data-ttu-id="525d6-152">다음 쿼리로 각 노드에서 사용 가능한 메모리에 대한 비슷한 꺾은선형 차트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="525d6-153">각 노드에 대해 사용 가능한 정확한 평균 값(MB)을 보여 주는 모든 노드에 대한 목록을 보려면 다음 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-153">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="525d6-155">c.</span><span class="sxs-lookup"><span data-stu-id="525d6-155">c.</span></span> <span data-ttu-id="525d6-156">시간별 평균, 최소, 최대 및 75 백분위 CPU 사용량을 검사하여 특정 노드로 드릴 다운하려는 경우 다음 쿼리(컴퓨터 필드 대체)를 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-156">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="525d6-158">[Operations Management Suite 블로그](https://blogs.technet.microsoft.com/msoms/tag/metrics/)의 Log Analytics에서 성능 메트릭에 대한 자세한 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="525d6-158">Read more information about performance metrics in Log Analytics at the [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-to-log-analytics"></a><span data-ttu-id="525d6-159">기존 저장소 계정을 Log Analytics에 추가</span><span class="sxs-lookup"><span data-stu-id="525d6-159">Adding an existing storage account to Log Analytics</span></span>

<span data-ttu-id="525d6-160">이 템플릿에서는 단순히 기존 저장소 계정을 신규 또는 기존 Log Analytics 작업 영역에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-160">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="525d6-161">[![Azure에 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="525d6-161">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="525d6-162">리소스 그룹 선택 시, 기존의 Log Analytics 작업 영역으로 작업 중인 경우 “기존 사용”을 선택하고 Log Analytics 작업 영역을 포함하는 리소스 그룹을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for the resource group containing the Log Analytics workspace.</span></span> <span data-ttu-id="525d6-163">그렇지 않은 경우 새 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="525d6-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="525d6-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="525d6-165">이 템플릿을 배포하면 Log Analytics 작업 영역에 연결된 저장소 계정을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-165">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span></span> <span data-ttu-id="525d6-166">이 인스턴스에서는 위에서 만든 Exchange 작업 영역에 하나 이상의 저장소 계정을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-166">In this instance, I added one more storage account to the Exchange workspace I created above.</span></span>
<span data-ttu-id="525d6-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="525d6-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="525d6-168">Service Fabric 이벤트 보기</span><span class="sxs-lookup"><span data-stu-id="525d6-168">View Service Fabric events</span></span>

<span data-ttu-id="525d6-169">배포를 완료하고 작업 영역에서 Service Fabric 솔루션을 사용하도록 설정했으면 Log Analytics 포털에서 **Service Fabric** 타일을 선택하여 Service Fabric 대시보드를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-169">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span></span> <span data-ttu-id="525d6-170">대시보드는 다음 표의 열을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-170">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="525d6-171">각 열은 지정된 시간 범위에 대한 열의 기준과 일치하는 카운트별로 상위 10개의 이벤트를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-171">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="525d6-172">각 열의 오른쪽 아래쪽에 있는 **모두 보기**를 클릭하거나 열 제목을 클릭하여 전체 목록을 제공하는 로그 검색을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-172">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="525d6-173">**Service Fabric 이벤트**</span><span class="sxs-lookup"><span data-stu-id="525d6-173">**Service Fabric event**</span></span> | <span data-ttu-id="525d6-174">**description**</span><span class="sxs-lookup"><span data-stu-id="525d6-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="525d6-175">주목할 만한 문제</span><span class="sxs-lookup"><span data-stu-id="525d6-175">Notable Issues</span></span> |<span data-ttu-id="525d6-176">RunAsyncFailures RunAsynCancellations 및 노드 다운 같은 문제를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="525d6-177">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="525d6-177">Operational Events</span></span> |<span data-ttu-id="525d6-178">응용 프로그램 업그레이드 및 배포와 같은 주목할 만한 작업 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="525d6-179">Reliable Service 이벤트</span><span class="sxs-lookup"><span data-stu-id="525d6-179">Reliable Service Events</span></span> |<span data-ttu-id="525d6-180">Runasyncinvocations와 같은 주목할 만한 Reliable Service 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="525d6-181">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="525d6-181">Actor Events</span></span> |<span data-ttu-id="525d6-182">행위자 메서드, 행위자 활성화 및 비활성화 등에 의해 throw된 예외와 같은 마이크로 서비스에 의해 생성된 주목할 만한 행위자 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="525d6-183">응용 프로그램 이벤트</span><span class="sxs-lookup"><span data-stu-id="525d6-183">Application Events</span></span> |<span data-ttu-id="525d6-184">응용 프로그램으로 생성된 모든 사용자 지정 ETW 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-184">All custom ETW events generated by your applications.</span></span> |

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="525d6-187">다음 표에서는 데이터 수집 방법 및 Service Fabric에 대해 데이터가 수집되는 방식에 대한 기타 세부 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-187">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="525d6-188">플랫폼</span><span class="sxs-lookup"><span data-stu-id="525d6-188">platform</span></span> | <span data-ttu-id="525d6-189">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="525d6-189">Direct Agent</span></span> | <span data-ttu-id="525d6-190">Operations Manager 에이전트</span><span class="sxs-lookup"><span data-stu-id="525d6-190">Operations Manager agent</span></span> | <span data-ttu-id="525d6-191">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="525d6-191">Azure Storage</span></span> | <span data-ttu-id="525d6-192">Operations Manager 필요 여부</span><span class="sxs-lookup"><span data-stu-id="525d6-192">Operations Manager required?</span></span> | <span data-ttu-id="525d6-193">관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="525d6-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="525d6-194">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="525d6-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="525d6-195">Windows</span><span class="sxs-lookup"><span data-stu-id="525d6-195">Windows</span></span> |  |  | <span data-ttu-id="525d6-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="525d6-196">&#8226;</span></span> |  |  |<span data-ttu-id="525d6-197">10분</span><span class="sxs-lookup"><span data-stu-id="525d6-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="525d6-198">대시보드 맨 위에서 **Data based on last 7 days(최근 7일에 따른 데이터)**를 클릭하여 Service Fabric 솔루션에서 이러한 이벤트 범위를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-198">You can change the scope of these events in the Service Fabric solution by clicking **Data based on last 7 days** at the top of the dashboard.</span></span> <span data-ttu-id="525d6-199">최근 7일, 1일 또는 6시간 내에 생성된 이벤트를 보여 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-199">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="525d6-200">또는 **사용자 지정**을 선택하고 사용자 지정 날짜 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-200">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="525d6-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="525d6-201">Next steps</span></span>

* <span data-ttu-id="525d6-202">[Log Analytics의 로그 검색](log-analytics-log-searches.md)을 사용하여 자세한 Service Fabric 이벤트 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="525d6-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
