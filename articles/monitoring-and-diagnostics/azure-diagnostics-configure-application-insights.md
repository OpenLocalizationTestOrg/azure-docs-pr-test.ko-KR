---
title: "Application Insights에 데이터를 보내도록 Azure 진단 구성 | Microsoft Docs"
description: "Application Insights에 데이터를 보내도록 Azure 진단 공용 구성을 업데이트 합니다."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 67dc2d5bbfa2012e4e098616edda593d023c4c1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="ad0b7-103">Application Insights에 클라우드 서비스, Virtual Machine 또는 Service Fabric 데이터 보내기</span><span class="sxs-lookup"><span data-stu-id="ad0b7-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="ad0b7-104">클라우드 서비스, Virtual Machines, 가상 컴퓨터 크기 집합 및 Service Fabric은 모두 Azure 진단 확장을 사용하여 데이터를 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="ad0b7-105">Azure 진단은 데이터를 Azure Storage 테이블에 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="ad0b7-106">그러나 Azure 진단 확장 1.5 이상을 사용하여 다른 위치에 데이터의 하위 집합이나 전체를 파이핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="ad0b7-107">이 문서에서는 Azure 진단 확장에서 Application Insights에 데이터를 전송하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="ad0b7-108">설명한 진단 구성</span><span class="sxs-lookup"><span data-stu-id="ad0b7-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="ad0b7-109">Azure 진단 확장 1.5는 진단 데이터를 보낼 수 있는 추가 위치인 싱크에 소개되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="ad0b7-110">Application Insights에 대한 싱크 예제 구성:</span><span class="sxs-lookup"><span data-stu-id="ad0b7-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="ad0b7-111">**싱크** *name* 특성은 싱크를 고유하게 식별하는 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="ad0b7-112">**ApplicationInsights** 요소는 Azure 진단 데이터를 보낼 Application Insights 리소스의 계측 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="ad0b7-113">기존 Application Insights 리소스가 없는 경우 리소스 만들기 및 계측 키 가져오기에 대한 자세한 내용은 [새 Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="ad0b7-114">Azure SDK 2.8 이상에서 클라우드 서비스를 개발하는 경우 이 계측 키는 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="ad0b7-115">클라우드 서비스 프로젝트를 패키징할 때 값은 **APPINSIGHTS_INSTRUMENTATIONKEY** 서비스 구성을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="ad0b7-116">[Application Insights를 Azure 진단과 함께 사용하여 클라우드 서비스 문제 해결](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="ad0b7-117">**채널** 요소는 하나 이상의 **채널** 요소를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="ad0b7-118">*name* 특성은 고유하게 해당 채널을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="ad0b7-119">*loglevel* 특성을 사용하면 채널이 허용하는 로그 수준을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="ad0b7-120">정보가 많은 순서대로 사용 가능한 로그 수준은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="ad0b7-121">자세한 정보 표시</span><span class="sxs-lookup"><span data-stu-id="ad0b7-121">Verbose</span></span>
        - <span data-ttu-id="ad0b7-122">정보</span><span class="sxs-lookup"><span data-stu-id="ad0b7-122">Information</span></span>
        - <span data-ttu-id="ad0b7-123">Warning</span><span class="sxs-lookup"><span data-stu-id="ad0b7-123">Warning</span></span>
        - <span data-ttu-id="ad0b7-124">오류</span><span class="sxs-lookup"><span data-stu-id="ad0b7-124">Error</span></span>
        - <span data-ttu-id="ad0b7-125">중요</span><span class="sxs-lookup"><span data-stu-id="ad0b7-125">Critical</span></span>

<span data-ttu-id="ad0b7-126">채널은 필터처럼 작동하고 채널을 사용하면 대상 싱크에 보내는 특정 로그 수준을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="ad0b7-127">예를 들어 자세한 정보 표시 로그를 수집하고 저장소에 보내지만 오류만을 싱크에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="ad0b7-128">다음 그래프에서는 이 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-128">The following graphic shows this relationship.</span></span>

![진단 공용 구성](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="ad0b7-130">다음 그래프에서는 구성 값 및 작동 방법을 요약합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="ad0b7-131">계층 구조에서 다양한 수준의 구성에 여러 싱크를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="ad0b7-132">최상위 수준의 싱크는 전역 설정이며 개별 요소에 지정된 싱크는 전역 설정에 재정의와 같은 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Application Insights를 사용한 진단 싱크 구성](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="ad0b7-134">전체 싱크 구성 예제</span><span class="sxs-lookup"><span data-stu-id="ad0b7-134">Complete sink configuration example</span></span>
<span data-ttu-id="ad0b7-135">다음은 공용 구성 파일의 완전한 예제로, 공용 구성 파일이 다음과 같은 작업을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="ad0b7-136">모든 오류를 Application Insights로 보냅니다(**DiagnosticMonitorConfiguration** 노드에서 지정).</span><span class="sxs-lookup"><span data-stu-id="ad0b7-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="ad0b7-137">또한 응용 프로그램 로그(**로그** 노드에서 지정함)에 대한 자세한 정보 표시 수준 로그를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
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
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="ad0b7-138">이전 구성에서 다음 줄은 다음과 같은 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="ad0b7-139">Azure 진단에서 수집한 모든 데이터 보내기</span><span class="sxs-lookup"><span data-stu-id="ad0b7-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="ad0b7-140">Application Insights 싱크로 오류 로그만 보내기</span><span class="sxs-lookup"><span data-stu-id="ad0b7-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="ad0b7-141">Application Insights에 자세한 정보 표시 응용 프로그램 로그 보내기</span><span class="sxs-lookup"><span data-stu-id="ad0b7-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="ad0b7-142">제한 사항</span><span class="sxs-lookup"><span data-stu-id="ad0b7-142">Limitations</span></span>

- <span data-ttu-id="ad0b7-143">**성능 카운터가 아닌 로그 유형인 채널**</span><span class="sxs-lookup"><span data-stu-id="ad0b7-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="ad0b7-144">성능 카운터 요소를 사용하여 채널을 지정하는 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="ad0b7-145">**채널에 대한 로그 수준은 Azure 진단에서 수집되는 로그 수준을 초과할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="ad0b7-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="ad0b7-146">예를 들어 로그 요소에서 응용 프로그램 로그 오류를 수집하고 Application Insight 싱크에 자세한 정보 표시 로그를 보내려고 시도할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="ad0b7-147">*scheduledTransferLogLevelFilter* 특성은 항상 싱크를 전송하려는 로그와 같거나 더 많은 로그를 수집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="ad0b7-148">**Application Insights에 Azure 진단 확장에서 수집된 Blob 데이터를 보낼 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="ad0b7-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="ad0b7-149">예를 들어 *디렉터리* 노드에 지정된 모든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="ad0b7-150">크래시 덤프의 경우 실제 크래시 덤프는 Blob Storage에 보내지고 크래시 덤프가 생성된 알림이 Application Insights에 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad0b7-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad0b7-151">Next Steps</span></span>
* <span data-ttu-id="ad0b7-152">Application Insights에서 [Azure 진단 정보를 보는 방법](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events)에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="ad0b7-153">[PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)을 사용하여 응용 프로그램에 대한 Azure 진단 확장을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="ad0b7-154">[Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) 를 사용하여 응용 프로그램에 대한 Azure 진단 확장을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad0b7-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
