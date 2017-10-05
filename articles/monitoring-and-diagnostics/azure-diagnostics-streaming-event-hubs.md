---
title: "Event Hubs를 사용하여 실행 부하 과다 경로에서 Azure 진단 데이터 스트리밍 | Microsoft 문서"
description: "일반적인 시나리오에 대한 지침을 포함하여 이벤트 허브로 Azure 진단을 완벽하게 구성."
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
ms.openlocfilehash: 1c05bd6dc4c4d394aa043b9995de9c184e4f14c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="6c756-103">이벤트 허브를 사용하여 실행 부하 과다 경로에서 Azure 진단 데이터 스트리밍</span><span class="sxs-lookup"><span data-stu-id="6c756-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="6c756-104">Azure 진단에서는 클라우드 서비스 VM(가상 컴퓨터)에서 메트릭 및 로그를 수집하고 결과를 Azure 저장소로 전송하는 유연한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="6c756-105">2016년 3월(SDK 2.9)부터 [Azure 이벤트 허브](https://azure.microsoft.com/services/event-hubs/)를 사용하여 데이터 원본을 사용자 지정하고 몇 초 만에 실행 부하 과다 경로 데이터를 전송할 수 있는 진단을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="6c756-106">지원되는 데이터 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-106">Supported data types include:</span></span>

* <span data-ttu-id="6c756-107">Windows (ETW) 이벤트에 대한 이벤트 추적</span><span class="sxs-lookup"><span data-stu-id="6c756-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="6c756-108">성능 카운터</span><span class="sxs-lookup"><span data-stu-id="6c756-108">Performance counters</span></span>
* <span data-ttu-id="6c756-109">Windows 이벤트 로그</span><span class="sxs-lookup"><span data-stu-id="6c756-109">Windows event logs</span></span>
* <span data-ttu-id="6c756-110">응용 프로그램 로그</span><span class="sxs-lookup"><span data-stu-id="6c756-110">Application logs</span></span>
* <span data-ttu-id="6c756-111">Azure 진단 인프라 로그</span><span class="sxs-lookup"><span data-stu-id="6c756-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="6c756-112">이 문서에서는 이벤트 허브에 Azure 진단을 구성하는 방법을 완벽하게 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="6c756-113">다음과 같은 일반적인 시나리오에 대한 지침도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="6c756-114">이벤트 허브에 전송된 로그 및 메트릭을 사용자 지정하는 방법</span><span class="sxs-lookup"><span data-stu-id="6c756-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="6c756-115">각 환경에서 구성을 변경하는 방법</span><span class="sxs-lookup"><span data-stu-id="6c756-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="6c756-116">이벤트 허브 스트림 데이터를 보는 방법</span><span class="sxs-lookup"><span data-stu-id="6c756-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="6c756-117">연결 문제를 해결하는 방법</span><span class="sxs-lookup"><span data-stu-id="6c756-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="6c756-118">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6c756-118">Prerequisites</span></span>
<span data-ttu-id="6c756-119">Azure 진단에서 데이터를 수신하는 이벤트 허브는 Azure SDK 2.9 및 해당 Visual Studio용 Azure 도구에서 시작하는 Cloud Services, VM, 가상 컴퓨터 확장 집합 및 Service Fabric에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="6c756-120">Azure 진단 확장 1.6(기본적으로[Azure SDK for .NET 2.9 이상](https://azure.microsoft.com/downloads/) 대상)</span><span class="sxs-lookup"><span data-stu-id="6c756-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="6c756-121">Visual Studio 2013 이상</span><span class="sxs-lookup"><span data-stu-id="6c756-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="6c756-122">*.wadcfgx* 파일과 다음 방법 중 하나를 사용하는 응용 프로그램에서 Azure 진단의 기존 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="6c756-123">Visual Studio: [Azure 클라우드 서비스 및 가상 컴퓨터에서 진단 구성](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="6c756-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="6c756-124">Windows PowerShell: [PowerShell을 사용하여 Azure 클라우드 서비스에서 진단 사용](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="6c756-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="6c756-125">항목별로 프로비전되는 Event Hubs 네임스페이스([Event Hubs 시작](../event-hubs/event-hubs-csharp-ephcs-getstarted.md) 참조)</span><span class="sxs-lookup"><span data-stu-id="6c756-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="6c756-126">이벤트 허브 싱크에 Azure 진단 연결</span><span class="sxs-lookup"><span data-stu-id="6c756-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="6c756-127">기본적으로 Azure 진단은 항상 Azure Storage 계정에 로그 및 메트릭을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="6c756-128">응용 프로그램은 *.wadcfgx* 파일의 **PublicConfig** / **WadCfg** 요소에 새로운 **Sinks** 섹션을 추가하여 이벤트 허브에 데이터를 전송할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="6c756-129">Visual Studio에서 *.wadcfgx* 파일은 **클라우드 서비스 프로젝트** > **역할** > **(RoleName)** > **diagnostics.wadcfgx** 파일이라는 경로에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="6c756-130">이 예제에서 이벤트 허브 URL은 이벤트 허브의 정규화된 네임스페이스(Event Hubs 네임스페이스 + “/” + 이벤트 허브 이름)로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="6c756-131">이벤트 허브 URL은 이벤트 허브 대시보드의 [Azure Portal](http://go.microsoft.com/fwlink/?LinkID=213885)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="6c756-132">**싱크** 이름의 경우 같은 값이 구성 파일 전체에서 일관되게 사용되고 있다면 유효한 문자열로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="6c756-133">이 섹션에서 구성된 *applicationInsights* 와 같은 추가 싱크가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="6c756-134">각 싱크가 **PrivateConfig** 섹션에서도 선언되어 있는 경우 Azure 진단을 통해 하나 이상의 싱크를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="6c756-135">또한, 이벤트 허브 싱크도 **.wadcfgx** 구성 파일의 *PrivateConfig* 섹션에서 선언되고 정의되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="6c756-136">`SharedAccessKeyName` 값은 **Event Hubs** 네임스페이스에 정의된 SAS(공유 액세스 서명) 키 및 정책과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-136">The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace.</span></span> <span data-ttu-id="6c756-137">[Azure Portal](https://manage.windowsazure.com)에서 Event Hubs 대시보드로 이동하여 **구성** 탭을 클릭하고 *보내기* 권한이 있는 명명된 정책(예: "SendRule")을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-137">Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="6c756-138">또한 **StorageAccount**도 **PrivateConfig**에서 선언되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="6c756-139">값이 작동 중인 경우 변경할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="6c756-140">이 예제에서는 값을 비워 둡니다. 이는 다운스트림 자산이 값을 설정한다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="6c756-141">예를 들어 *ServiceConfiguration.Cloud.cscfg* 환경 구성 파일은 환경에 적절한 이름 및 키를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="6c756-142">이벤트 허브 SAS 키는 *.wadcfgx* 파일에 일반 텍스트로 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="6c756-143">이 키는 때로 소스 코드 제어에서 발견되거나 빌드 서버에서 자산으로 사용할 수 있는 경우가 있으므로 적절하게 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="6c756-144">악의적인 사용자가 SAS 키를 이벤트 허브에 작성하기만 하고 수신하거나 관리하지 않을 수 있으므로 여기서 *보내기 전용* 권한으로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="6c756-145">Azure 진단을 구성하여 이벤트 허브에 로그 및 메트릭 전송</span><span class="sxs-lookup"><span data-stu-id="6c756-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="6c756-146">이전에 설명한 대로 모든 기본 및 사용자 지정 진단 데이터(예: 메트릭 및 로그)는 구성된 간격으로 Azure Storage로 자동 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="6c756-147">이벤트 허브 및 추가 싱크를 사용하여 이벤트 허브로 전송될 계층 구조에서 루트 또는 리프 노드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="6c756-148">여기에는 ETW 이벤트, 성능 카운터, Windows 이벤트 로그 및 응용 프로그램 로그가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="6c756-149">얼마나 많은 데이터 요소를 실제로 이벤트 허브로 전송해야 하는지 고려하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="6c756-150">일반적으로 개발자는 신속하게 사용하고 해석해야 하는 대기 시간이 짧은 실행 부하 과다 경로 데이터를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="6c756-151">예는 경고를 모니터링하고 규칙을 자동 크기 조정하는 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="6c756-152">개발자는 대체 분석 또는 검색 저장소(예: Azure 스트림 분석, ElasticSearch, 사용자 지정 모니터링 시스템 또는 즐겨찾는 타사 모니터링 시스템)를 구성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="6c756-153">다음은 몇 가지 구성 예입니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-153">The following are some example configurations.</span></span>

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

<span data-ttu-id="6c756-154">위의 예제에서는 싱크가 계층 구조에서 부모 **PerformanceCounters** 노드에 적용됩니다. 즉 모든 자식 **PerformanceCounters**를 Event Hubs로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-154">In the above example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

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

<span data-ttu-id="6c756-155">이전 예제에서 싱크는 단 세 개의 카운터(**대기 중인 요청**, **거부된 요청** 및 **% 프로세서 시간**)에만 적용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="6c756-156">다음 예제에서는 개발자가 전송될 데이터 양을 이 서비스의 상태에 사용되는 중요 메트릭으로 제한하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="6c756-157">이 예제에서 싱크는 로그에 적용되며 오류 수준 추적으로만 필터링됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="6c756-158">클라우드 서비스 응용 프로그램과 진단 구성 배포 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="6c756-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="6c756-159">Visual Studio에서는 응용 프로그램 및 이벤트 허브 싱크 구성을 배포하는 가장 쉬운 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="6c756-160">파일을 보고 편집하려면 Visual Studio에서 *.wadcfgx* 파일을 열고 편집하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="6c756-161">경로는 **클라우드 서비스 프로젝트** > **역할** > **(RoleName)** > **diagnostics.wadcfgx**입니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="6c756-162">이 시점에서 Visual Studio의 모든 배포 및 배포 업데이트 작업, Visual Studio Team System 및 MSBuild에 기반하고 **/t:publish** 대상을 사용하는 모든 명령 또는 스크립트에는 패키징 프로세스에 있는 *.wadcfgx* 가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="6c756-163">또한 배포 및 업데이트는 VM에서 적절한 Azure 진단 에이전트 확장을 사용하여 파일을 Azure에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="6c756-164">응용 프로그램 및 Azure 진단 구성을 배포한 후에 이벤트 허브의 대시보드에서 즉시 작업을 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="6c756-165">이것은 사용자가 선택한 분석 도구 또는 수신기 클라이언트에서 실행 부하 과다 경로 데이터를 볼 준비가 되었다는 것을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="6c756-166">다음 그림에서 이벤트 허브 대시보드는 오후 11시 이후에 시작하는 이벤트 허브에 진단 데이터를 정상적으로 보내는 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="6c756-167">이 때 응용 프로그램이 업데이트된 *.wadcfgx* 파일과 함께 배포되고 싱크가 올바르게 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="6c756-168">Azure 진단 구성 파일(.wadcfgx)을 업데이트할 경우 Visual Studio 게시 또는 Windows PowerShell 스크립트를 사용하여 구성 뿐만 아니라 전체 응용 프로그램에 대한 업데이트를 푸시하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="6c756-169">실행 부하 과다 경로 데이터 보기</span><span class="sxs-lookup"><span data-stu-id="6c756-169">View hot-path data</span></span>
<span data-ttu-id="6c756-170">이전에 설명한 대로 이벤트 허브 데이터를 수신하고 처리하는 많은 사용 사례가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="6c756-171">한 가지 간단한 접근 방법은 이벤트 허브를 수신하고 출력 스트림을 인쇄하기 위한 작은 테스트 콘솔 응용 프로그램을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="6c756-172">[Event Hubs 시작](../event-hubs/event-hubs-csharp-ephcs-getstarted.md) 문서에서 자세히 설명하는 다음 코드를 콘솔 응용 프로그램에 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="6c756-173">콘솔 응용 프로그램에는 [이벤트 프로세서 호스트 NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/)가 포함되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="6c756-174">**기본** 함수에서 꺾쇠 괄호로 묶인 값을 리소스에 사용할 값으로 바꾸십시오.</span><span class="sxs-lookup"><span data-stu-id="6c756-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

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

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="6c756-175">이벤트 허브 싱크 문제 해결</span><span class="sxs-lookup"><span data-stu-id="6c756-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="6c756-176">이벤트 허브가 들어오거나 나가는 이벤트 활동을 예상대로 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="6c756-177">이벤트 허브가 성공적으로 프로비저닝되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="6c756-178">**.wadcfgx** 의 *PrivateConfig* 섹션에 있는 모든 연결 정보는 포털에서 보이는 리소스의 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="6c756-179">포털에 정의된 SAS 정책(예에서는 "SendRule")이 있고 *보내기* 권한이 부여되도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="6c756-180">업데이트 이후에 이벤트 허브는 들어오거나 나가는 이벤트 작업을 더 이상 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="6c756-181">우선 이벤트 허브 및 구성 정보가 이전에 설명한 대로 정확한지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="6c756-182">때로는 배포 업데이트에서 **PrivateConfig** 가 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="6c756-183">권장되는 해결 방법은 프로젝트에서 *.wadcfgx* 에 모든 변경 사항을 적용한 다음 전체 응용 프로그램 업데이트를 푸시하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="6c756-184">불가능한 경우 진단 업데이트가 SAS 키를 포함하여 전체 **PrivateConfig** 를 푸시하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="6c756-185">제안된 방법을 시도했지만 이벤트 허브가 여전히 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="6c756-186">Azure 진단 자체에 대한 로그 및 오류가 포함된 Azure 저장소 테이블( **WADDiagnosticInfrastructureLogsTable**)을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="6c756-187">한 가지 옵션은 [Azure 저장소 탐색기](http://www.storageexplorer.com) 등의 도구를 사용하여 이 저장소 계정에 연결하고 이 테이블을 본 후 지난 24시간 동안의 타임스탬프에 대한 쿼리를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="6c756-188">이 도구를 사용하여 .csv 파일을 내보내고 Microsoft Excel과 같은 응용 프로그램에서 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="6c756-189">Excel를 통해 어떤 오류가 보고되는지 확인하는 **EventHubs**와 같은 전화 카드 문자열을 쉽게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6c756-190">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c756-190">Next steps</span></span>
<span data-ttu-id="6c756-191">• [Event Hubs에 대해 자세히 알아보기](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="6c756-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="6c756-192">부록: Azure 진단 구성 파일(.wadcfgx) 예제 완료</span><span class="sxs-lookup"><span data-stu-id="6c756-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="6c756-193">이 예제에 대한 보조 *ServiceConfiguration.Cloud.cscfg* 는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

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

<span data-ttu-id="6c756-194">가상 컴퓨터에 대한 Json 기반 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c756-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="6c756-195">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6c756-195">Next steps</span></span>
<span data-ttu-id="6c756-196">Event Hubs에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c756-196">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="6c756-197">이벤트 허브 개요</span><span class="sxs-lookup"><span data-stu-id="6c756-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="6c756-198">이벤트 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="6c756-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="6c756-199">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="6c756-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
