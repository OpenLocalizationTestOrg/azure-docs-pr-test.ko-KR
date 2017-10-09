---
title: "Azure 진단을 사용 하 여 로그 aaaCollect | Microsoft Docs"
description: "이 문서에서는 Azure에서 실행 되는 서비스 패브릭 클러스터에서 Azure 진단을 toocollect tooset 기록 하는 방법을 설명 합니다."
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
ms.openlocfilehash: afbcfbe972b1847ef33bf0539b4398794b1bd56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a><span data-ttu-id="09895-103">Azure 진단을 사용하여 로그 수집</span><span class="sxs-lookup"><span data-stu-id="09895-103">Collect logs by using Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09895-104">Windows</span><span class="sxs-lookup"><span data-stu-id="09895-104">Windows</span></span>](service-fabric-diagnostics-how-to-setup-wad.md)
> * [<span data-ttu-id="09895-105">Linux</span><span class="sxs-lookup"><span data-stu-id="09895-105">Linux</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

<span data-ttu-id="09895-106">Azure 서비스 패브릭 클러스터를 실행 하는 경우 중앙 위치에 있는 모든 hello 노드에서 것이 좋습니다 toocollect hello가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="09895-107">Hello 로그를 중앙 위치에 있는 분석 및 클러스터의 문제 또는 hello 응용 프로그램 및 해당 클러스터에서 실행 되는 서비스의 문제를 해결 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09895-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="09895-108">한 가지 방법은 tooupload 및 수집 로그는 업로드 로그 저장소, Azure Application Insights 또는 Azure 이벤트 허브 tooAzure toouse hello Azure 진단 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-108">One way tooupload and collect logs is toouse hello Azure Diagnostics extension, which uploads logs tooAzure Storage, Azure Application Insights, or Azure Event Hubs.</span></span> <span data-ttu-id="09895-109">hello 로그는 저장소에서 직접 또는 이벤트 허브에 그다지 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-109">hello logs are not that useful directly in storage or in Event Hubs.</span></span> <span data-ttu-id="09895-110">저장소에서 외부 프로세스 tooread hello 이벤트를 사용 하 고와 같은 제품에 배치할 수 있습니다 하지만 [로그 분석](../log-analytics/log-analytics-service-fabric.md) 또는 다른 로그 구문 분석 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-110">But you can use an external process tooread hello events from storage and place them in a product such as [Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span> <span data-ttu-id="09895-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)에는 포괄적인 로그 검색 및 분석 서비스가 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="09895-111">[Azure Application Insights](https://azure.microsoft.com/services/application-insights/) comes with a comprehensive log search and analytics service built-in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09895-112">필수 조건</span><span class="sxs-lookup"><span data-stu-id="09895-112">Prerequisites</span></span>
<span data-ttu-id="09895-113">이러한 도구 tooperform를 사용 하 여이 문서에서 hello 작업의 일부:</span><span class="sxs-lookup"><span data-stu-id="09895-113">You use these tools tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="09895-114">[Azure 진단](../cloud-services/cloud-services-dotnet-diagnostics.md) (관련 클라우드 서비스 tooAzure 않았으나 좋은 정보 및 예제)</span><span class="sxs-lookup"><span data-stu-id="09895-114">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="09895-115">Azure 리소스 관리자</span><span class="sxs-lookup"><span data-stu-id="09895-115">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="09895-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="09895-116">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="09895-117">Azure Resource Manager 클라이언트</span><span class="sxs-lookup"><span data-stu-id="09895-117">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="09895-118">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="09895-118">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-sources-that-you-might-want-toocollect"></a><span data-ttu-id="09895-119">Toocollect 알았으므로 로그 원본</span><span class="sxs-lookup"><span data-stu-id="09895-119">Log sources that you might want toocollect</span></span>
* <span data-ttu-id="09895-120">**서비스 패브릭 로그**: hello 플랫폼 toostandard 이벤트 추적에 대 한 ETW (Windows) 및 EventSource 채널에서 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-120">**Service Fabric logs**: Emitted from hello platform toostandard Event Tracing for Windows (ETW) and EventSource channels.</span></span> <span data-ttu-id="09895-121">로그는 여러 유형 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-121">Logs can be one of several types:</span></span>
  * <span data-ttu-id="09895-122">작업 이벤트: hello 서비스 패브릭 플랫폼을 수행 하는 작업에 대 한 로그입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-122">Operational events: Logs for operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="09895-123">응용 프로그램 및 서비스 만들기, 노드 상태 변경, 업그레이드 정보 등을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-123">Examples include creation of applications and services, node state changes, and upgrade information.</span></span>
  * [<span data-ttu-id="09895-124">Reliable Actors 프로그래밍 모델 이벤트</span><span class="sxs-lookup"><span data-stu-id="09895-124">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="09895-125">Reliable Services 프로그래밍 모델 이벤트</span><span class="sxs-lookup"><span data-stu-id="09895-125">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)
* <span data-ttu-id="09895-126">**응용 프로그램 이벤트**: hello Visual Studio 서식 파일에서 제공 하는 hello EventSource 도우미 클래스를 사용 하 여 기록 및 서비스의 코드에서 발생 하는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-126">**Application events**: Events emitted from your service's code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="09895-127">응용 프로그램에서 toowrite 기록 하는 방법에 대 한 자세한 내용은 참조 하십시오. [모니터 하 고 서비스는 로컬 컴퓨터 개발 설정에서 진단](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-127">For more information on how toowrite logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="09895-128">Hello 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="09895-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="09895-129">로그를 수집 hello 첫 번째 단계는 hello 서비스 패브릭 클러스터에 있는 hello Vm의 각 toodeploy hello 진단 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="09895-130">hello 진단 확장 각 VM에서 로그를 수집 하 고 사용자가 지정한 toohello 저장소 계정으로 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="09895-131">hello 단계 hello Azure 포털 또는 Azure 리소스 관리자를 사용 하는 여부에 따라 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="09895-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="09895-132">또한 hello 단계 hello 배포의 클러스터 생성의 일부 인지 또는 이미 존재 하는 클러스터에 대 한 인지에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="09895-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="09895-133">각 시나리오에 대 한 hello 단계를 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-hello-portal"></a><span data-ttu-id="09895-134">Hello 포털을 통해 클러스터 만들기의 일부로 hello 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="09895-134">Deploy hello Diagnostics extension as part of cluster creation through hello portal</span></span>
<span data-ttu-id="09895-135">hello 다음 이미지에 표시 된 hello 진단 설정 패널을 사용 하면 toodeploy hello 진단 확장 toohello Vm 클러스터 만들기의 일부로 hello 클러스터의.</span><span class="sxs-lookup"><span data-stu-id="09895-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image.</span></span> <span data-ttu-id="09895-136">Reliable Actors 또는 신뢰할 수 있는 서비스 이벤트 수집 tooenable 진단 너무 설정 되어 있는지 확인**에** (기본 설정 hello).</span><span class="sxs-lookup"><span data-stu-id="09895-136">tooenable Reliable Actors or Reliable Services event collection, ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="09895-137">Hello 클러스터를 만드는 hello 포털을 사용 하 여 이러한 설정을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-137">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![클러스터 만들기에 대 한 hello 포털의 azure 진단 설정](./media/service-fabric-diagnostics-how-to-setup-wad/portal-cluster-creation-diagnostics-setting.png)

<span data-ttu-id="09895-139">Azure 지원 팀 hello *필요* 지원 toohelp 해결 만드는 모든 지원 요청을 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-139">hello Azure support team *requires* support logs toohelp resolve any support requests that you create.</span></span> <span data-ttu-id="09895-140">이러한 로그는 실시간으로 수집 하 고 hello 리소스 그룹에 생성 된 hello 저장소 계정 중 하나에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09895-140">These logs are collected in real time and are stored in one of hello storage accounts created in hello resource group.</span></span> <span data-ttu-id="09895-141">hello 진단 설정은 응용 프로그램 수준 이벤트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-141">hello Diagnostics settings configure application-level events.</span></span> <span data-ttu-id="09895-142">이 이벤트를 포함할 [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) 이벤트 [신뢰할 수 있는 서비스](service-fabric-reliable-services-diagnostics.md) 이벤트 및 Azure 저장소에 저장 된 일부 시스템 수준 서비스 패브릭 이벤트 toobe 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-142">These events include [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) events, [Reliable Services](service-fabric-reliable-services-diagnostics.md) events, and some system-level Service Fabric events toobe stored in Azure Storage.</span></span>

<span data-ttu-id="09895-143">와 같은 제품 [Elasticsearch](https://www.elastic.co/guide/index.html) 하거나 hello 저장소 계정에서 사용자가 소유한 프로세스 hello 이벤트를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-143">Products such as [Elasticsearch](https://www.elastic.co/guide/index.html) or your own process can get hello events from hello storage account.</span></span> <span data-ttu-id="09895-144">Ľ ř ˝ 방법은 toofilter 또는 그루 밍 hello 이벤트가 toohello 테이블 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09895-144">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="09895-145">Hello 테이블에서 프로세스 tooremove 이벤트를 구현 하지 않는 경우 hello 테이블 toogrow를 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09895-145">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span>

<span data-ttu-id="09895-146">Hello 포털을 사용 하 여 클러스터를 만들 때 매우 권장 hello 서식 파일을 다운로드 하는 **클릭 하기 전에** toocreate hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-146">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="09895-147">자세한 내용은 참조 너무[Azure 리소스 관리자 템플릿을 사용 하 여 서비스 패브릭 클러스터를 설정](service-fabric-cluster-creation-via-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-147">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="09895-148">일부 변경 내용은 hello 포털을 사용 하 여 변경할 수 없으므로 나중 hello 템플릿 toomake 변경 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-148">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

<span data-ttu-id="09895-149">단계를 수행 하는 hello를 사용 하 여 hello 포털에서 서식 파일을 내보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-149">You can export templates from hello portal by using hello following steps.</span></span> <span data-ttu-id="09895-150">그러나 이러한 템플릿은 필요한 정보를 누락 된 null 값 포함 될 수 있으므로 더 어렵게 toouse 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-150">However, these templates can be more difficult toouse because they might have null values that are missing required information.</span></span>

1. <span data-ttu-id="09895-151">리소스 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="09895-151">Open your resource group.</span></span>
2. <span data-ttu-id="09895-152">선택 **설정을** toodisplay hello 설정 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-152">Select **Settings** toodisplay hello settings panel.</span></span>
3. <span data-ttu-id="09895-153">선택 **배포** toodisplay hello 배포 기록 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-153">Select **Deployments** toodisplay hello deployment history panel.</span></span>
4. <span data-ttu-id="09895-154">Hello 배포는 배포 toodisplay hello 세부 사항을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-154">Select a deployment toodisplay hello details of hello deployment.</span></span>
5. <span data-ttu-id="09895-155">선택 **템플릿 내보내기** toodisplay hello 템플릿 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-155">Select **Export Template** toodisplay hello template panel.</span></span>
6. <span data-ttu-id="09895-156">선택 **toofile 저장** tooexport hello 템플릿, 매개 변수, 및 PowerShell 파일을 포함 하는.zip 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-156">Select **Save toofile** tooexport a .zip file that contains hello template, parameter, and PowerShell files.</span></span>

<span data-ttu-id="09895-157">Hello 파일을 내보낸 후 toomake 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-157">After you export hello files, you need toomake a modification.</span></span> <span data-ttu-id="09895-158">Hello parameters.json 파일을 편집 하 고 hello 제거 **adminPassword** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-158">Edit hello parameters.json file and remove hello **adminPassword** element.</span></span> <span data-ttu-id="09895-159">이렇게 하면 hello 암호에 대 한 프롬프트 hello 배포 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-159">This will cause a prompt for hello password when hello deployment script is run.</span></span> <span data-ttu-id="09895-160">Hello 배포 스크립트를 실행 하는 경우에 toofix null 매개 변수 값을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-160">When you're running hello deployment script, you might have toofix null parameter values.</span></span>

<span data-ttu-id="09895-161">템플릿 tooupdate는 구성을 다운로드 하는 toouse hello:</span><span class="sxs-lookup"><span data-stu-id="09895-161">toouse hello downloaded template tooupdate a configuration:</span></span>

1. <span data-ttu-id="09895-162">로컬 컴퓨터의 hello 내용 tooa 폴더를 추출 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-162">Extract hello contents tooa folder on your local computer.</span></span>
2. <span data-ttu-id="09895-163">Hello 내용을 tooreflect hello 새 구성을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-163">Modify hello contents tooreflect hello new configuration.</span></span>
3. <span data-ttu-id="09895-164">PowerShell을 시작 하 고 hello 콘텐츠를 추출한 toohello 폴더를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-164">Start PowerShell and change toohello folder where you extracted hello content.</span></span>
4. <span data-ttu-id="09895-165">실행 **deploy.ps1** hello 구독 ID, hello 리소스 그룹 이름 입력 (사용 하 여 hello 동일한 이름 tooupdate hello 구성), 및 고유 배포 이름을 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-165">Run **deploy.ps1** and fill in hello subscription ID, hello resource group name (use hello same name tooupdate hello configuration), and a unique deployment name.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="09895-166">Azure 리소스 관리자를 사용 하 여 클러스터 생성의 일환으로 hello 진단 확장을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-166">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="09895-167">리소스 관리자를 사용 하 여 클러스터 toocreate 있어야만 tooadd hello 진단 구성 JSON toohello 전체 클러스터 리소스 관리자 템플릿 hello 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="09895-167">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="09895-168">추가 진단 구성을 사용 하 여 샘플 5-V 클러스터 리소스 관리자 템플릿을 제공 tooit 리소스 관리자 템플릿 샘플의 일부분으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-168">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="09895-169">이 위치 hello Azure 샘플 갤러리에서 확인할 수 있습니다.: [진단 리소스 관리자 템플릿 샘플 5 개 노드 클러스터](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-169">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype).</span></span>

<span data-ttu-id="09895-170">hello 리소스 관리자 템플릿, 열기 hello azuredeploy.json 파일 및 검색에서 toosee hello 진단 설정을 **IaaSDiagnostics**합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-170">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="09895-171">이 서식 파일을 선택 하는 hello를 사용 하 여 클러스터 toocreate **tooAzure 배포** hello 이전 링크에서 사용할 수 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-171">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="09895-172">또는 hello 리소스 관리자 예제 추가 정보 다운로드, 변경 내용을 tooit 만들고 수 hello를 사용 하 여 hello 수정 된 템플릿을 사용 하 여 클러스터를 만들 `New-AzureRmResourceGroupDeployment` Azure PowerShell 창에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-172">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="09895-173">Hello toohello 명령에 전달 하는 hello 매개 변수에 대 한 코드 다음을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="09895-173">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="09895-174">PowerShell을 사용 하 여 리소스 toodeploy 그룹화 하는 방법에 대 한 자세한 내용은 hello 문서 참조 [hello Azure 리소스 관리자 템플릿 사용 하 여 리소스 그룹 배포](../azure-resource-manager/resource-group-template-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-174">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

```powershell

New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -Name $deploymentName -TemplateFile $pathToARMConfigJsonFile -TemplateParameterFile $pathToParameterFile –Verbose
```

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="09895-175">Hello 진단 확장 tooan 기존 클러스터 배포</span><span class="sxs-lookup"><span data-stu-id="09895-175">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="09895-176">기존 클러스터를 배포 하는 진단이 없는 경우 또는 toomodify 기존 구성 하려는 경우 추가 하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-176">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="09895-177">Hello 리소스 관리자 템플릿을 사용 하는 toocreate hello 기존 클러스터를 수정 하거나 hello 템플릿을 앞에서 설명한 대로 hello 포털에서 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-177">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="09895-178">Hello 다음 작업을 수행 하 여 hello template.json 파일을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-178">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="09895-179">Toohello 리소스 섹션을 추가 하 여 새 저장소 리소스 toohello 서식 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-179">Add a new storage resource toohello template by adding toohello resources section.</span></span>

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

 <span data-ttu-id="09895-180">다음으로, 중간 hello 저장소 계정 정의 바로 뒤 섹션 toohello 매개 변수를 추가 `supportLogStorageAccountName` 및 `vmNodeType0Name`합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-180">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="09895-181">Hello 개체 틀 텍스트 바꾸기 *저장소 계정 이름 입력* hello hello 저장소 계정의 이름으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-181">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="09895-182">그런 다음 업데이트 hello `VirtualMachineProfile` hello 코드 hello 확장 배열 내에서 다음을 추가 하 여 hello template.json 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-182">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="09895-183">있는지 tooadd hello 시작 이나 삽입 되는 위치에 따라 hello 끝 쉼표 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-183">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

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

<span data-ttu-id="09895-184">설명 된 대로 hello template.json 파일을 수정한 후에 hello 리소스 관리자 템플릿을 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-184">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="09895-185">Hello 서식 파일을 내보낸 경우 실행 중인 hello deploy.ps1 파일 hello 템플릿을 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-185">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="09895-186">배포 후에는 **ProvisioningState**가 **성공**했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-186">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="update-diagnostics-toocollect-health-and-load-events"></a><span data-ttu-id="09895-187">진단 toocollect 상태 및 부하 이벤트 업데이트</span><span class="sxs-lookup"><span data-stu-id="09895-187">Update diagnostics toocollect health and load events</span></span>

<span data-ttu-id="09895-188">릴리스부터 hello 5.4 서비스 패브릭의 상태 및 부하 메트릭 이벤트는 컬렉션에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09895-188">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="09895-189">이러한 이벤트 hello 상태를 사용 하 여 hello 시스템 또는 사용자 코드에 의해 생성 된 이벤트를 반영 하거나 보고 Api와 같은 로드 [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) 또는 [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-189">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="09895-190">이를 통해 시간 경과에 따른 시스템 상태의 집계 및 확인과 상태 또는 부하 이벤트 기반의 경고가 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-190">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="09895-191">이러한 Visual Studio의 진단 이벤트 뷰어의이 이벤트에에서 추가 tooview "Microsoft-ServiceFabric:4:0x4000000000000008" toohello ETW 공급자 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-191">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="09895-192">toocollect hello 이벤트 hello 리소스 관리자 템플릿 tooinclude 수정</span><span class="sxs-lookup"><span data-stu-id="09895-192">toocollect hello events, modify hello resource manager template tooinclude</span></span>

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

## <a name="update-diagnostics-toocollect-and-upload-logs-from-new-eventsource-channels"></a><span data-ttu-id="09895-193">진단 toocollect를 업데이트 하 고 새 EventSource 채널에서 로그 업로드</span><span class="sxs-lookup"><span data-stu-id="09895-193">Update Diagnostics toocollect and upload logs from new EventSource channels</span></span>
<span data-ttu-id="09895-194">hello hello와 같이 동일한 단계를 수행 하는 toodeploy에 대 한 사용자가 있는 새 응용 프로그램을 나타내는 새 EventSource 채널에서 tooupdate 진단 toocollect 로그 [이전 섹션](#deploywadarm) 진단의 기존 설치에 대 한 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-194">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as in hello [previous section](#deploywadarm) for setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="09895-195">Hello 업데이트 `EtwEventSourceProviderConfiguration` hello 새로운 EventSource 채널 hello 구성을 적용 하기 전에 hello를 사용 하 여 업데이트에 대 한 hello template.json 파일 tooadd 항목 섹션 `New-AzureRmResourceGroupDeployment` PowerShell 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="09895-195">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="09895-196">hello 이벤트 소스의 hello 이름 hello ServiceEventSource.cs Visual Studio에서 생성 된 파일에 코드의 일부로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="09895-196">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="09895-197">예를 들어 이벤트 원본이 Eventsource 내 이름이 이면 hello MyDestinationTableName 라는 테이블로 tooplace hello 이벤트 코드 Eventsource 내에서 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-197">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="09895-198">toocollect 성능 카운터 또는 이벤트 로그에서 제공 하는 hello 예제를 사용 하 여 hello 리소스 관리자 템플릿을 수정 [는Azure리소스관리자템플릿을사용하여Windows가상컴퓨터를모니터링및진단을작성](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="09895-198">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="09895-199">그런 다음 hello 리소스 관리자 템플릿을 다시 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-199">Then, republish hello Resource Manager template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09895-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="09895-200">Next steps</span></span>
<span data-ttu-id="09895-201">자세히 toounderstand 문제를 해결 하는 동안 확인 해야 할 이벤트 참조에 대 한 내보내는 hello 진단 이벤트 [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) 및 [신뢰할 수 있는 서비스](service-fabric-reliable-services-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="09895-201">toounderstand in more detail what events you should look for while troubleshooting issues, see hello diagnostic events emitted for [Reliable Actors](service-fabric-reliable-actors-diagnostics.md) and [Reliable Services](service-fabric-reliable-services-diagnostics.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="09895-202">관련 문서</span><span class="sxs-lookup"><span data-stu-id="09895-202">Related articles</span></span>
* [<span data-ttu-id="09895-203">Toocollect 성능 카운터 또는 로그를 사용 하 여 hello 진단 확장 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="09895-203">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="09895-204">Log Analytics의 Service Fabric 솔루션</span><span class="sxs-lookup"><span data-stu-id="09895-204">Service Fabric solution in Log Analytics</span></span>](../log-analytics/log-analytics-service-fabric.md)

