---
title: "서비스 패브릭 이벤트 집계 Linux Azure 진단으로 aaaAzure | Microsoft Docs"
description: "Azure Service Fabric 클러스터 모니터링 및 진단을 위해 LAD를 사용하여 이벤트를 집계 및 수집하는 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a><span data-ttu-id="85c00-103">Linux Azure 진단을 사용하여 이벤트 집계 및 수집</span><span class="sxs-lookup"><span data-stu-id="85c00-103">Event aggregation and collection using Linux Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85c00-104">Windows</span><span class="sxs-lookup"><span data-stu-id="85c00-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="85c00-105">Linux</span><span class="sxs-lookup"><span data-stu-id="85c00-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="85c00-106">Azure 서비스 패브릭 클러스터를 실행 하는 경우 중앙 위치에 있는 모든 hello 노드에서 것이 좋습니다 toocollect hello가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="85c00-107">Hello 로그를 중앙 위치에 있는 분석 및 클러스터의 문제 또는 hello 응용 프로그램 및 해당 클러스터에서 실행 되는 서비스의 문제를 해결 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="85c00-108">한 가지 방법은 tooupload 및 수집 로그는 로그 tooAzure 저장소에 업로드 하 고 hello 옵션 toosend 로그 tooAzure Application Insights 또는 이벤트 허브에는 toouse hello Linux Azure 진단 (했다) 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-108">One way tooupload and collect logs is toouse hello Linux Azure Diagnostics (LAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="85c00-109">저장소에서 외부 프로세스 tooread hello 이벤트를 사용 하 고와 같은 분석 플랫폼 제품에 배치할 수도 있습니다 [OMS 로그 분석](../log-analytics/log-analytics-service-fabric.md) 또는 다른 로그 구문 분석 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="log-and-event-sources"></a><span data-ttu-id="85c00-110">로그 및 이벤트 원본</span><span class="sxs-lookup"><span data-stu-id="85c00-110">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="85c00-111">Service Fabric 플랫폼 이벤트</span><span class="sxs-lookup"><span data-stu-id="85c00-111">Service Fabric platform events</span></span>
<span data-ttu-id="85c00-112">Service Fabric은 운영 이벤트 또는 런타임 이벤트를 포함하여 [LTTng](http://lttng.org)를 통해 몇 가지 기본 제공 로그를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-112">Service Fabric emits a few out-of-the-box logs via [LTTng](http://lttng.org), including operational events or runtime events.</span></span> <span data-ttu-id="85c00-113">이러한 로그는 서식 파일을 지정 하는 클러스터의 리소스 관리자 hello hello 위치에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-113">These logs are stored in hello location that hello cluster's Resource Manager template specifies.</span></span> <span data-ttu-id="85c00-114">tooget hello 태그에 대 한 검색을 hello 저장소 계정 세부 정보를 설정 또는 **AzureTableWinFabETWQueryable** 를 찾아서 **StoreConnectionString**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-114">tooget or set hello storage account details, search for hello tag **AzureTableWinFabETWQueryable** and look for **StoreConnectionString**.</span></span>

### <a name="application-events"></a><span data-ttu-id="85c00-115">응용 프로그램 이벤트</span><span class="sxs-lookup"><span data-stu-id="85c00-115">Application events</span></span>
 <span data-ttu-id="85c00-116">소프트웨어를 계측할 때 지정한 대로 응용 프로그램 및 서비스 코드에서 발생되는 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-116">Events emitted from your applications' and services' code as specified by you when instrumenting your software.</span></span> <span data-ttu-id="85c00-117">텍스트 기반 로그 파일을 작성하는 모든 로깅 솔루션을 사용할 수 있습니다(예: LTTng).</span><span class="sxs-lookup"><span data-stu-id="85c00-117">You can use any logging solution that writes text-based log files--for example, LTTng.</span></span> <span data-ttu-id="85c00-118">자세한 내용은 응용 프로그램 추적에서 hello LTTng 설명서를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-118">For more information, see hello LTTng documentation on tracing your application.</span></span>

<span data-ttu-id="85c00-119">[로컬 컴퓨터 개발 설정에서의 모니터링 및 진단 서비스](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)</span><span class="sxs-lookup"><span data-stu-id="85c00-119">[Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="85c00-120">Hello 진단 확장 배포</span><span class="sxs-lookup"><span data-stu-id="85c00-120">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="85c00-121">로그를 수집 hello 첫 번째 단계는 hello 서비스 패브릭 클러스터에 있는 hello Vm의 각 toodeploy hello 진단 확장입니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-121">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="85c00-122">hello 진단 확장 각 VM에서 로그를 수집 하 고 사용자가 지정한 toohello 저장소 계정으로 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-122">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="85c00-123">hello 단계 hello Azure 포털 또는 Azure 리소스 관리자를 사용 하는지 여부에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-123">hello steps vary based on whether you use hello Azure portal or Azure Resource Manager.</span></span>

<span data-ttu-id="85c00-124">클러스터 만들기의 일부로 hello 클러스터의 toodeploy hello 진단 확장 toohello Vm 설정 **진단** 너무**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-124">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, set **Diagnostics** too**On**.</span></span> <span data-ttu-id="85c00-125">Hello 클러스터를 만드는 hello 포털을 사용 하 여이 설정을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-125">After you create hello cluster, you can't change this setting by using hello portal.</span></span>

<span data-ttu-id="85c00-126">그런 다음 Linux Azure 진단 (했다) toocollect hello 파일을 구성 하 고 저장소 계정에 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-126">Then, configure Linux Azure Diagnostics (LAD) toocollect hello files and place them into your storage account.</span></span> <span data-ttu-id="85c00-127">이 과정은 시나리오에 해당 3 ("업로드 하세요. 로그 파일을 직접") hello 문서에 설명 되어 [를 사용 하 여 했다 toomonitor 고 Linux Vm의 경우 진단](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-127">This process is explained as scenario 3 ("Upload your own log files") in hello article [Using LAD toomonitor and diagnose Linux VMs](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="85c00-128">추적 프로세스 다가갈 수 있고, toohello 액세스를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-128">Following this process gets you access toohello traces.</span></span> <span data-ttu-id="85c00-129">사용자가 선택한 hello 추적 tooa 시각화 도우미를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-129">You can upload hello traces tooa visualizer of your choice.</span></span>

<span data-ttu-id="85c00-130">또한 Azure 리소스 관리자를 사용 하 여 hello 진단 확장을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-130">You can also deploy hello Diagnostics extension by using Azure Resource Manager.</span></span> <span data-ttu-id="85c00-131">hello 프로세스는 Windows 및 Linux에 대 한 유사 하며 Windows에서 클러스터에 대 한 설명 [toocollect Azure 진단으로 기록 하는 방법을](service-fabric-diagnostics-how-to-setup-wad.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-131">hello process is similar for Windows and Linux and is documented for Windows clusters in [How toocollect logs with Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md).</span></span>

<span data-ttu-id="85c00-132">또한 [Linux와 함께 사용하는 Operations Management Suite Log Analytics](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/)에 설명된 대로 Operations Management Suite를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-132">You can also use Operations Management Suite, as described in [Operations Management Suite Log Analytics with Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).</span></span>

<span data-ttu-id="85c00-133">이 구성에서는 완료 된 후 hello 했다 에이전트 모니터링 hello 로그 파일을 지정된 합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-133">After you finish this configuration, hello LAD agent monitors hello specified log files.</span></span> <span data-ttu-id="85c00-134">때마다 새 줄에는 추가 된 toohello 파일에는 사용자가 지정한 보낸된 toohello 저장소 syslog 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-134">Whenever a new line is appended toohello file, it creates a syslog entry that is sent toohello storage that you specified.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85c00-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="85c00-135">Next steps</span></span>

<span data-ttu-id="85c00-136">자세히 toounderstand 문제를 해결 하는 동안 검사 해야 이벤트 참조 [LTTng 설명서](http://lttng.org/docs) 및 [를 사용 하 여 했다](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="85c00-136">toounderstand in more detail what events you should examine while troubleshooting issues, see [LTTng documentation](http://lttng.org/docs) and [Using LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>
