---
title: "이벤트 허브를 사용 하 여 hello 실행 부하 과다 경로에 Azure 진단 데이터 aaaStreaming | Microsoft Docs"
description: "이벤트 허브와 Azure 진단 구성 tooend, 일반적인 시나리오에 대 한 지침을 포함 하 여 종료 합니다."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="9baf7-103">이벤트 허브를 사용 하 여 hello 실행 부하 과다 경로에 Azure 진단 데이터를 스트리밍</span><span class="sxs-lookup"><span data-stu-id="9baf7-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="9baf7-104">Azure 진단 유연한 방법이 toocollect 메트릭을 제공 하 고에서 기록 클라우드 서비스 Vm (가상 컴퓨터) 및 결과 tooAzure 저장소를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="9baf7-105">Hello 2016 년 3 월 (SDK 2.9) 시간 내에 부터는 진단 toocustom 데이터 소스를 보내고 수 (초)를 사용 하 여 실행 부하 과다 경로 데이터를 전송 [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="9baf7-106">지원되는 데이터 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-106">Supported data types include:</span></span>

* <span data-ttu-id="9baf7-107">Windows (ETW) 이벤트에 대한 이벤트 추적</span><span class="sxs-lookup"><span data-stu-id="9baf7-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="9baf7-108">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="9baf7-108">Performance counters</span></span>
* <span data-ttu-id="9baf7-109">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="9baf7-109">Windows event logs</span></span>
* <span data-ttu-id="9baf7-110">응용 프로그램 로그</span><span class="sxs-lookup"><span data-stu-id="9baf7-110">Application logs</span></span>
* <span data-ttu-id="9baf7-111">Azure 진단 인프라 로그</span><span class="sxs-lookup"><span data-stu-id="9baf7-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="9baf7-112">이 문서에서 이벤트 허브를 사용 하 여 Azure 진단 tooconfigure tooend를 종료 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="9baf7-113">다음 일반적인 시나리오는 hello에 대 한 지침이 제공도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="9baf7-114">Toocustomize hello 기록 하는 방법 및 tooEvent 허브 전송 하는 메트릭</span><span class="sxs-lookup"><span data-stu-id="9baf7-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="9baf7-115">어떻게 각 환경에 toochange 구성</span><span class="sxs-lookup"><span data-stu-id="9baf7-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="9baf7-116">Tooview 이벤트 허브에 데이터를 스트림 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9baf7-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="9baf7-117">Tootroubleshoot 연결 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="9baf7-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="9baf7-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9baf7-118">Prerequisites</span></span>
<span data-ttu-id="9baf7-119">Azure 진단에서 이벤트 허브 receieving 데이터는 클라우드 서비스, Vm, 가상 컴퓨터 크기 집합 및 Azure SDK 2.9 hello 및 Azure Tools for Visual Studio에 해당 하는 hello 부터는 서비스 패브릭에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="9baf7-120">Azure 진단 확장 1.6(기본적으로[Azure SDK for .NET 2.9 이상](https://azure.microsoft.com/downloads/) 대상)</span><span class="sxs-lookup"><span data-stu-id="9baf7-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="9baf7-121">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="9baf7-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="9baf7-122">사용 하 여 응용 프로그램에서 Azure 진단의 기존 구성은 *.wadcfgx* 파일과 hello 메서드를 다음 중 하나:</span><span class="sxs-lookup"><span data-stu-id="9baf7-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="9baf7-123">Visual Studio: [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="9baf7-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="9baf7-124">Windows PowerShell: [PowerShell을 사용하여 Azure 클라우드 서비스에서 진단 사용](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="9baf7-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="9baf7-125">이벤트 허브 네임 스페이스 hello 아티클 단위의 프로 비전 [이벤트 허브 시작](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="9baf7-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="9baf7-126">Azure 진단 tooEvent 허브 싱크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="9baf7-127">기본적으로 Azure 진단 로그 및 메트릭 tooan Azure 저장소 계정에 항상 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="9baf7-128">추가 하 여 데이터 tooEvent 허브 응용 프로그램에 보낼 수도 있습니다 **싱크** hello 섹션 **PublicConfig** / **WadCfg** hello 요소의*.wadcfgx* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="9baf7-129">Visual Studio에서 hello *.wadcfgx* 파일 경로 따라 hello에 저장 됩니다: **클라우드 서비스 프로젝트** > **역할** > **드 ( RoleName)** > **diagnostics.wadcfgx** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

<span data-ttu-id="9baf7-130">이 예제에서는 URL이 toohello를 완벽 하 게 설정 하는 hello 이벤트 허브 정규화 된 네임 스페이스 hello 이벤트 허브의: 이벤트 허브 네임 스페이스 + "/" + 이벤트 허브 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="9baf7-131">URL hello에 표시 되는 hello 이벤트 허브 [Azure 포털](http://go.microsoft.com/fwlink/?LinkID=213885) hello 이벤트 허브 대시보드에서.</span><span class="sxs-lookup"><span data-stu-id="9baf7-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="9baf7-132">hello **싱크** 이름을 설정할 수 있습니다 tooany 유효한 문자열 hello 동일한 값이 사용 일관 되 게 hello 구성 파일 전체으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="9baf7-133">이 섹션에서 구성된 *applicationInsights* 와 같은 추가 싱크가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="9baf7-134">Azure 진단을 허용 또는 toobe hello에 각 싱크를 선언 하는 경우 정의 된 싱크 자세히 **PrivateConfig** 섹션.</span><span class="sxs-lookup"><span data-stu-id="9baf7-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="9baf7-135">hello 이벤트 허브 싱크도 여야 선언 하며 hello에 정의 된 **PrivateConfig** hello 섹션 *.wadcfgx* 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

<span data-ttu-id="9baf7-136">hello `SharedAccessKeyName` 공유 액세스 서명 (SAS) 키와 hello에 정의 된 정책 값과 일치 해야 **이벤트 허브** 네임 스페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="9baf7-137">Hello에서 이벤트 허브 대시보드 toohello 찾아보기 [Azure 포털](https://manage.windowsazure.com), hello 클릭 **구성** 탭 하 고 있는 명명 된 정책 (예: "SendRule")를 설정 *보낼* 사용 권한입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="9baf7-138">hello **StorageAccount** 에 선언 됩니다 **PrivateConfig**합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="9baf7-139">없어도 여기 toochange 값 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="9baf7-140">이 예제에서는 상태로 두면 hello 값 비어 있는 다운스트림 자산 hello 값을 설정 하는 기호입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="9baf7-141">예를 들어 hello *ServiceConfiguration.Cloud.cscfg* 환경 구성 파일 hello 환경에 적합 한 이름 및 키로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="9baf7-142">hello 이벤트 허브 SAS 키가 hello에 일반 텍스트로 저장 *.wadcfgx* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="9baf7-143">종종이 키 toosource 코드 제어에서 체크 또는 적절 하 게 보호 해야 하므로 빌드 서버에 자산으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="9baf7-144">사용 하 여 여기에 SAS 키를 사용 하는 것이 좋습니다 *보내기만* 권한을 악의적인 사용자 또는 수 있도록 toohello 이벤트 허브를 작성 하지만 하지 tooit 수신 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="9baf7-145">Azure 진단 toosend 로그 및 메트릭 tooEvent 허브 구성</span><span class="sxs-lookup"><span data-stu-id="9baf7-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="9baf7-146">이전에 설명한 대로, 모든 기본 및 사용자 지정 진단 데이터 즉, 메트릭 및 로그를 자동으로 전송 됩니다 tooAzure 저장소 hello 구성 된 간격으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="9baf7-147">이벤트 허브와 추가 싱크 hello 계층 toobe 전송 toohello 이벤트 허브의에서 모든 루트 또는 리프 노드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="9baf7-148">여기에는 ETW 이벤트, 성능 카운터, Windows 이벤트 로그 및 응용 프로그램 로그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="9baf7-149">데이터 요소 실제로 해야 tooconsider tooEvent 허브 전송 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="9baf7-150">일반적으로 개발자는 신속하게 사용하고 해석해야 하는 대기 시간이 짧은 실행 부하 과다 경로 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="9baf7-151">예는 경고를 모니터링하고 규칙을 자동 크기 조정하는 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="9baf7-152">개발자는 대체 분석 또는 검색 저장소(예: Azure 스트림 분석, ElasticSearch, 사용자 지정 모니터링 시스템 또는 즐겨찾는 타사 모니터링 시스템)를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="9baf7-153">hello 다음은 몇 가지 예제 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-153">hello following are some example configurations.</span></span>

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

<span data-ttu-id="9baf7-154">위 예제는 hello, hello 싱크는 적용 된 toohello 부모 **PerformanceCounters** 즉, 모든 자식 hello 계층의 노드에 **PerformanceCounters** tooEvent 허브 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

<span data-ttu-id="9baf7-155">Hello 이전 예에서 hello 싱크는 적용 된 tooonly 카운터가 세 개: **Requests Queued**, **요청이 거부**, 및 **% 프로세서 시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="9baf7-156">hello 다음 예제 방법을 개발자 보낸된 데이터 toobe hello 중요 한 메트릭이이 서비스의이 상태에 사용 되는 양을 hello를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

<span data-ttu-id="9baf7-157">이 예제에서는 hello 싱크 적용된 toologs 이며 필터링 된 유일한 tooerror 수준 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="9baf7-158">클라우드 서비스 응용 프로그램과 진단 구성 배포 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="9baf7-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="9baf7-159">Visual Studio hello 쉬운 경로 toodeploy hello 응용 프로그램 및 이벤트 허브 싱크 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="9baf7-160">tooview 및 편집 hello 파일을 열고 hello *.wadcfgx* Visual Studio에서 파일, 편집 및 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="9baf7-161">hello 경로가 **클라우드 서비스 프로젝트** > **역할** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="9baf7-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="9baf7-162">이 시점에서 모든 배포 및 배포는 Visual Studio, Visual Studio Team System 및 모든 명령 또는 스크립트 hello를 사용 하 여 MSBuild를 기반으로 작업 업데이트 **/t: 게시** 대상 포함 hello *.wadcfgx*  hello 패키징 프로세스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="9baf7-163">또한, 배포 및 업데이트 hello 파일 tooAzure Vm에서 적절 한 Azure 진단 에이전트가 확장 hello를 사용 하 여 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="9baf7-164">Hello 응용 프로그램 및 Azure 진단 구성, 배포 hello 대시보드에서 hello 이벤트 허브의 활동을에서 즉시 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="9baf7-165">이 사용자가 선택한 hello 수신기 클라이언트 또는 분석 도구에서 tooviewing hello 실행 부하 과다 경로 데이터에 대해 준비 toomove 하 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="9baf7-166">다음 그림 hello, hello 이벤트 허브 대시보드에 정상 보내는 진단 데이터 toohello 이벤트 허브 시작 오후 11 시 완료 된 후 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="9baf7-167">이 경우에 hello 응용 프로그램이 배포 되었는지와 업데이트 된 *.wadcfgx* 파일을 찾아 hello 싱크가 제대로 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="9baf7-168">업데이트 toohello Azure 진단 구성 파일 (.wadcfgx)을 수행 하면 hello 구성 뿐만 아니라 hello 업데이트 toohello 전체 응용 프로그램 Visual Studio 게시 또는 Windows PowerShell 스크립트를 사용 하 여 푸시 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="9baf7-169">실행 부하 과다 경로 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="9baf7-169">View hot-path data</span></span>
<span data-ttu-id="9baf7-170">이전에 설명한 대로는 이벤트 허브 데이터를 처리 하는 수신 대기 tooand 많은 사례가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="9baf7-171">한 가지 간단한 방법은 toocreate 작은 테스트 콘솔 응용 프로그램 toolisten toohello 이벤트 허브 및 인쇄 hello 출력 스트림에 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="9baf7-172">코드에서 더 자세하게에서 설명 된 다음 hello를 배치할 수 [이벤트 허브 시작](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), 콘솔 응용 프로그램에서입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="9baf7-173">콘솔 응용 프로그램 hello hello에 포함 해야 [이벤트 프로세서 호스트 NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="9baf7-174">꺾쇠 괄호의 hello tooreplace hello 값 기억 **Main** 리소스에 대 한 값으로 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="9baf7-175">이벤트 허브 싱크 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9baf7-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="9baf7-176">이벤트 허브 hello 들어오거나 나가는 이벤트 작업이 예상 대로 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="9baf7-177">이벤트 허브가 성공적으로 프로비저닝되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="9baf7-178">모든 연결 정보 hello에 **PrivateConfig** 섹션 *.wadcfgx* hello 포털에서와 같이 리소스의 hello 값과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="9baf7-179">SAS 정책 정의 (hello 예제에서 "SendRule")에 해당 하며 hello 포털 갖도록 *보낼* 권한이 부여 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="9baf7-180">업데이트 후 더 이상 hello 이벤트 허브 들어오거나 나가는 이벤트 활동을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="9baf7-181">먼저, hello 이벤트 허브 및 구성 정보가 이전에 설명한 대로 정확한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="9baf7-182">경우에 따라 hello **PrivateConfig** 배포 업데이트에서 다시 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="9baf7-183">수정 프로그램은 모든 너무 변경 내용 toomake hello 권장*.wadcfgx* 프로젝트 hello와 완전 한 응용 프로그램 업데이트를 푸시하고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="9baf7-184">없는 경우 해당 hello 진단 업데이트 푸시 전체 있는지 확인 **PrivateConfig** hello SAS 키를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="9baf7-185">Hello 제안 했으나 hello 이벤트 허브 여전히 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="9baf7-186">Azure 진단 프로그램 자체에 대 한 로그 및 오류를 포함 하는 hello Azure 저장소 테이블에서 찾아보십시오: **WADDiagnosticInfrastructureLogsTable**합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="9baf7-187">한 가지 옵션은 toouse와 같은 도구 [Azure 저장소 탐색기](http://www.storageexplorer.com) tooconnect toothis 저장소 계정에이 테이블을 한에 쿼리를 추가 타임 스탬프에 대 한 hello 지난 24 시간 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="9baf7-188">Hello 도구 tooexport.csv 파일을 사용할 수 있으며 Microsoft Excel과 같은 응용 프로그램에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="9baf7-189">Excel을 사용 하면 전화 카드 문자열에 대 한 쉬운 toosearch 같은 **EventHubs**, toosee 어떤 오류가 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="9baf7-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9baf7-190">Next steps</span></span>
<span data-ttu-id="9baf7-191">• [Event Hubs에 대해 자세히 알아보기](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="9baf7-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="9baf7-192">부록: Azure 진단 구성 파일(.wadcfgx) 예제 완료</span><span class="sxs-lookup"><span data-stu-id="9baf7-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

<span data-ttu-id="9baf7-193">hello 상호 보완적인 *ServiceConfiguration.Cloud.cscfg* 이 예제에서는 다음과 같은 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="9baf7-194">가상 컴퓨터에 대한 Json 기반 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="9baf7-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9baf7-195">Next steps</span></span>
<span data-ttu-id="9baf7-196">Hello 다음 링크를 방문 하 여 이벤트 허브에 대 한 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9baf7-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="9baf7-197">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="9baf7-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="9baf7-198">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="9baf7-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="9baf7-199">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="9baf7-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
