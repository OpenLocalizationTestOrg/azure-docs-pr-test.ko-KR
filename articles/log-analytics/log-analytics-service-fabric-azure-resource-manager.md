---
title: "로그 분석에 사용 하 여 서비스 패브릭 응용 프로그램 aaaAssess hello Azure 포털 | Microsoft Docs"
description: "Hello 서비스 패브릭 솔루션을 사용 하 여 hello Azure 포털 tooassess hello 위험 및 서비스 패브릭 응용 프로그램의 상태를 사용 하 여 로그 분석에서 마이크로 서비스, 노드 및 클러스터입니다."
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
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="493d9-103">서비스 패브릭 응용 프로그램 및 Azure 포털 hello로 마이크로 서비스를 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="493d9-104">리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="493d9-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="493d9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="493d9-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Service Fabric 기호](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="493d9-107">이 문서에서는 toouse hello 로그 분석 toohelp에서 서비스 패브릭 솔루션을 식별 하 고 서비스 패브릭 클러스터 전체에서 문제를 해결 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="493d9-108">서비스 패브릭 솔루션 hello Azure WAD 테이블에서이 데이터를 수집 하 여 서비스 패브릭 Vm에서 Azure 진단 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="493d9-109">그러면 Log Analytics에서는 **Reliable Service 이벤트**, **행위자 이벤트**, **작업 이벤트**, **사용자 지정 ETW 이벤트**를 포함한 Service Fabric 프레임워크 이벤트를 읽어옵니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="493d9-110">Hello 솔루션 대시보드를 함께 수 tooview 주목할 만한 문제 및 관련 이벤트 서비스 패브릭 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="493d9-111">tooconnect 해야 tooget hello 솔루션 시작, 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="493d9-112">다음은 세 가지 시나리오 tooconsider가입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="493d9-113">서비스 패브릭 클러스터를 배포 하지 않은 경우의 hello 단계를 사용 하 여 ***연결 된 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역 배포*** toodeploy 새 클러스터 tooreport tooLog 분석 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="493d9-114">필요한 경우 toocollect ÷ ´ ֹ 호스트 toouse에서 보안과 같은 다른 OMS 솔루션 서비스 패브릭 클러스터를에서 다음과 같이 hello ***VM 확장과 연결 된 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역 배포 설치합니다.***</span><span class="sxs-lookup"><span data-stu-id="493d9-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="493d9-115">서비스 패브릭 클러스터를 이미 배포한 경우 및 tooconnect 원하는 것 tooLog 분석, hello 단계에 따라 ***기존 저장소 계정 tooLog 분석을 추가 합니다.***</span><span class="sxs-lookup"><span data-stu-id="493d9-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="493d9-116">연결 된 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="493d9-117">이 서식 파일은 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-117">This template does hello following:</span></span>

1. <span data-ttu-id="493d9-118">Azure 서비스 패브릭 클러스터를 이미 연결 되어 tooa 로그 분석 작업 영역을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="493d9-119">Hello 옵션 toocreate는 새 작업 영역이 있는 hello 템플릿이나 입력된 hello 이름을 이미 기존 로그 분석 작업 영역을 배포 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="493d9-120">Hello 진단 저장소 계정 toohello 로그 분석 작업 영역을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="493d9-121">로그 분석 작업 영역에서 hello 서비스 패브릭 솔루션을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="493d9-122">[![TooAzure 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="493d9-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="493d9-123">선택 하 고 나면 hello 위의 단추를 배포, hello Azure 포털이 열리면 tooedit 있습니다에 대 한 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="493d9-124">새 로그 분석 작업 영역 이름을 입력 하는 경우 있는지 toocreate 새 리소스 그룹을 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="493d9-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![서비스 패브릭](./media/log-analytics-service-fabric/2.png)

![서비스 패브릭](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="493d9-127">Hello 약관에 동의 하 고 클릭 **만들기** toostart hello 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="493d9-128">새 작업 영역 hello 및 클러스터를 만든 참조 하 고 WADServiceFabric hello 해야 hello 배포가 완료 되 면 * 추가 된 이벤트, WADWindowsEventLogs 및 WADETWEvent 테이블:</span><span class="sxs-lookup"><span data-stu-id="493d9-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![서비스 패브릭](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="493d9-130">VM 확장 설치에 연결 된 서비스 패브릭 클러스터 tooa 로그 분석 작업 영역을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="493d9-131">이 서식 파일은 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-131">This template does hello following:</span></span>

1. <span data-ttu-id="493d9-132">Azure 서비스 패브릭 클러스터를 이미 연결 되어 tooa 로그 분석 작업 영역을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="493d9-133">새 작업 영역을 만들거나 기존 작업 영역을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="493d9-134">Hello 진단 저장소 계정 toohello 로그 분석 작업 영역을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="493d9-135">Hello 로그 분석 작업 영역에서 hello 서비스 패브릭 솔루션을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="493d9-136">서비스 패브릭 클러스터에 설정 하는 각 가상 컴퓨터 크기에 hello MMA agent 확장을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="493d9-137">Hello MMA 에이전트를 설치, 해당 노드에 대 한 수 tooview 성능 메트릭이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="493d9-138">[![TooAzure 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="493d9-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="493d9-139">다음 입력된 hello 필요한 매개 변수 위의 동일한 단계를 hello 및 배포를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="493d9-140">다시 한 번 hello 새 작업 영역, 클러스터 및 생성된 된 모든 WAD 테이블 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![서비스 패브릭](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="493d9-142">성능 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="493d9-142">Viewing Performance Data</span></span>

<span data-ttu-id="493d9-143">성능 데이터를 프로그램 노드에서 tooview:</span><span class="sxs-lookup"><span data-stu-id="493d9-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="493d9-144">Hello Azure 포털에서에서 hello 로그 분석 작업 영역을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="493d9-145">![서비스 패브릭](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="493d9-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="493d9-146">TooSettings hello 왼쪽된 창에서 이동 하 고 데이터 선택 >> Windows 성능 카운터 >> "추가 hello 선택한 성능 카운터": ![서비스 패브릭](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="493d9-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="493d9-147">로그 검색에 사용 하 여 hello 다음에 해당 노드에 대 한 주요 메트릭을 toodelve를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="493d9-148">a.</span><span class="sxs-lookup"><span data-stu-id="493d9-148">a.</span></span> <span data-ttu-id="493d9-149">비교의 노드를 문제가 있는 hello 마지막 1 시간 toosee 프로그램 모든 노드에서 평균 CPU 사용률 hello 했으며 어떤 시간 간격 노드 스파이크가:</span><span class="sxs-lookup"><span data-stu-id="493d9-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="493d9-151">b.</span><span class="sxs-lookup"><span data-stu-id="493d9-151">b.</span></span> <span data-ttu-id="493d9-152">다음 쿼리로 각 노드에서 사용 가능한 메모리에 대한 비슷한 꺾은선형 차트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="493d9-153">이 쿼리를 사용 하는 각 노드에 대 한 사용 가능한 공간 (mb)에 대 한 hello 정확한 평균 값을 표시 하면 모든 노드 목록이 tooview:</span><span class="sxs-lookup"><span data-stu-id="493d9-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="493d9-155">c.</span><span class="sxs-lookup"><span data-stu-id="493d9-155">c.</span></span> <span data-ttu-id="493d9-156">Hello 시간별 평균을 검사 하 여 특정 노드로 아래로 toodrill를 원하는 hello 경우 최소, 최대 및 75 백분위 수 CPU 사용 하는 수 toodo 하 여이이 쿼리 (대체 컴퓨터 필드)를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="493d9-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![서비스 패브릭](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="493d9-158">Hello에 로그 분석에서 성능 메트릭에 대 한 자세한 내용을 살펴볼 [Operations Management Suite 블로그](https://blogs.technet.microsoft.com/msoms/tag/metrics/)합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="493d9-159">기존 저장소 계정 tooLog 분석 추가</span><span class="sxs-lookup"><span data-stu-id="493d9-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="493d9-160">이 서식 파일에는 단순히 기존 저장소 계정을 tooa 새로운 또는 기존 로그 분석 작업 영역에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="493d9-161">[![TooAzure 배포](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="493d9-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="493d9-162">리소스 그룹 선택에 이미 기존 로그 분석 작업 영역을 사용 하는 경우 "기존 테이블 사용" 및 선택 hello 로그 분석 작업 영역을 포함 하는 hello 리소스 그룹에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="493d9-163">그렇지 않은 경우 새 작업 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="493d9-164">![서비스 패브릭](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="493d9-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="493d9-165">이 서식 파일을 배포한 후 수 toosee hello 저장소 계정 연결 tooyour 로그 분석 작업 영역 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="493d9-166">이 인스턴스에서 하나 이상의 저장소 계정 toohello Exchange 작업 영역 I 위에서 만든 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="493d9-167">![서비스 패브릭](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="493d9-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="493d9-168">Service Fabric 이벤트 보기</span><span class="sxs-lookup"><span data-stu-id="493d9-168">View Service Fabric events</span></span>

<span data-ttu-id="493d9-169">Hello 배포 완료 되 면 hello 솔루션 서비스 패브릭 작업 영역에서 설정 되어 선택 hello **서비스 패브릭** hello 로그 분석 포털 toolaunch hello 서비스 패브릭 대시보드 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="493d9-170">hello 대시보드는 다음 표에 hello에 hello 열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="493d9-171">각 열 개수를 비교 하 hello에 대 한 열의 기준을 시간 범위를 지정 하 여 hello 상위 10 개의 이벤트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="493d9-172">클릭 하 여 hello 전체 목록을 제공 하는 로그 검색을 실행할 수 있습니다 **스크롤하게** 각 열의 또는 hello 열 머리글을 클릭 하 여 hello 오른쪽 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="493d9-173">**Service Fabric 이벤트**</span><span class="sxs-lookup"><span data-stu-id="493d9-173">**Service Fabric event**</span></span> | <span data-ttu-id="493d9-174">**description**</span><span class="sxs-lookup"><span data-stu-id="493d9-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="493d9-175">주목할 만한 문제</span><span class="sxs-lookup"><span data-stu-id="493d9-175">Notable Issues</span></span> |<span data-ttu-id="493d9-176">RunAsyncFailures RunAsynCancellations 및 노드 다운 같은 문제를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="493d9-177">작업 이벤트</span><span class="sxs-lookup"><span data-stu-id="493d9-177">Operational Events</span></span> |<span data-ttu-id="493d9-178">응용 프로그램 업그레이드 및 배포와 같은 주목할 만한 작업 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="493d9-179">Reliable Service 이벤트</span><span class="sxs-lookup"><span data-stu-id="493d9-179">Reliable Service Events</span></span> |<span data-ttu-id="493d9-180">Runasyncinvocations와 같은 주목할 만한 Reliable Service 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="493d9-181">행위자 이벤트</span><span class="sxs-lookup"><span data-stu-id="493d9-181">Actor Events</span></span> |<span data-ttu-id="493d9-182">행위자 메서드, 행위자 활성화 및 비활성화 등에 의해 throw된 예외와 같은 마이크로 서비스에 의해 생성된 주목할 만한 행위자 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="493d9-183">응용 프로그램 이벤트</span><span class="sxs-lookup"><span data-stu-id="493d9-183">Application Events</span></span> |<span data-ttu-id="493d9-184">응용 프로그램으로 생성된 모든 사용자 지정 ETW 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-184">All custom ETW events generated by your applications.</span></span> |

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric 대시보드](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="493d9-187">hello 다음 표에서 데이터 수집 방법과 서비스 패브릭에 대 한 데이터 수집 방법에 대 한 기타 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="493d9-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="493d9-188">플랫폼</span><span class="sxs-lookup"><span data-stu-id="493d9-188">platform</span></span> | <span data-ttu-id="493d9-189">직접 에이전트</span><span class="sxs-lookup"><span data-stu-id="493d9-189">Direct Agent</span></span> | <span data-ttu-id="493d9-190">Operations Manager 에이전트</span><span class="sxs-lookup"><span data-stu-id="493d9-190">Operations Manager agent</span></span> | <span data-ttu-id="493d9-191">Azure 저장소</span><span class="sxs-lookup"><span data-stu-id="493d9-191">Azure Storage</span></span> | <span data-ttu-id="493d9-192">Operations Manager 필요 여부</span><span class="sxs-lookup"><span data-stu-id="493d9-192">Operations Manager required?</span></span> | <span data-ttu-id="493d9-193">관리 그룹을 통해 전송되는 Operations Manager 에이전트 데이터</span><span class="sxs-lookup"><span data-stu-id="493d9-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="493d9-194">수집 빈도</span><span class="sxs-lookup"><span data-stu-id="493d9-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="493d9-195">Windows</span><span class="sxs-lookup"><span data-stu-id="493d9-195">Windows</span></span> |  |  | <span data-ttu-id="493d9-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="493d9-196">&#8226;</span></span> |  |  |<span data-ttu-id="493d9-197">10분</span><span class="sxs-lookup"><span data-stu-id="493d9-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="493d9-198">클릭 하 여 hello 서비스 패브릭 솔루션에서에서 이러한 이벤트의 hello 범위를 변경할 수 **지난 7 일을 기준으로 데이터** hello hello 대시보드 위쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="493d9-199">6 시간 또는 1 일, 지난 7 일 hello 내에서 생성 된 이벤트를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="493d9-200">선택할 수 있습니다 또는 **사용자 지정** toospecify 사용자 지정 날짜 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="493d9-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="493d9-201">Next steps</span></span>

* <span data-ttu-id="493d9-202">사용 하 여 [로그 분석에서 로그 검색](log-analytics-log-searches.md) tooview 서비스 패브릭 이벤트 데이터를 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="493d9-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
