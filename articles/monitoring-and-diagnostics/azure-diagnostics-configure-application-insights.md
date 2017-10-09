---
title: "aaaConfigure Azure 진단 toosend 데이터 tooApplication Insights | Microsoft Docs"
description: "Hello Azure 진단 공용 구성 toosend 데이터 tooApplication 통찰력을 업데이트 합니다."
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
ms.openlocfilehash: 7c36f29da8fdc12fa58c17458348a311b900b0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a><span data-ttu-id="93ff4-103">클라우드 서비스, 가상 컴퓨터 또는 서비스 패브릭 진단 데이터 tooApplication Insights 보내기</span><span class="sxs-lookup"><span data-stu-id="93ff4-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data tooApplication Insights</span></span>
<span data-ttu-id="93ff4-104">가상 컴퓨터, 가상 컴퓨터 크기 집합 및 서비스 패브릭 모든 클라우드 서비스는 hello Azure 진단 확장 toocollect 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use hello Azure Diagnostics extension toocollect data.</span></span>  <span data-ttu-id="93ff4-105">Azure 진단 데이터 tooAzure 저장소 테이블을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-105">Azure diagnostics sends data tooAzure Storage tables.</span></span>  <span data-ttu-id="93ff4-106">그러나 수도 있습니다 모든 파이프 또는 Azure 진단 확장 1.5 이상을 사용 하 여 hello 데이터 tooother 위치의 하위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-106">However, you can also pipe all or a subset of hello data tooother locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="93ff4-107">이 문서에서는 toosend 데이터를 Azure 진단 확장 tooApplication Insights hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-107">This article describes how toosend data from hello Azure Diagnostics extension tooApplication Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="93ff4-108">설명한 진단 구성</span><span class="sxs-lookup"><span data-stu-id="93ff4-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="93ff4-109">진단 데이터를 보낼 수 있는 추가 위치는 Azure 진단 확장 1.5 도입 된 싱크를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-109">hello Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="93ff4-110">Application Insights에 대한 싱크 예제 구성:</span><span class="sxs-lookup"><span data-stu-id="93ff4-110">Example configuration of a sink for Application Insights:</span></span>

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
- <span data-ttu-id="93ff4-111">hello **싱크** *이름* 특성은 hello 싱크를 고유 하 게 식별 하는 문자열 값입니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-111">hello **Sink** *name* attribute is a string value that uniquely identifies hello sink.</span></span>

- <span data-ttu-id="93ff4-112">hello **ApplicationInsights** 요소 hello hello Azure 진단 데이터를 보내는 위치 Application insights 리소스의 계측 키를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-112">hello **ApplicationInsights** element specifies instrumentation key of hello Application insights resource where hello Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="93ff4-113">기존 Application Insights 리소스를 설정 하지 않은 경우 참조 [새 Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md) 리소스 만들기 및 hello 계측 키 가져오기에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting hello instrumentation key.</span></span>
    - <span data-ttu-id="93ff4-114">Azure SDK 2.8 이상에서 클라우드 서비스를 개발하는 경우 이 계측 키는 자동으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="93ff4-115">hello 값은 hello 기반 **APPINSIGHTS_INSTRUMENTATIONKEY** hello 클라우드 서비스 프로젝트를 패키지할 때 서비스 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-115">hello value is based on hello **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging hello Cloud Service project.</span></span> <span data-ttu-id="93ff4-116">참조 [Azure 진단 tootroubleshoot 있는 Application Insights를 사용 하 여 클라우드 서비스는 발급](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-116">See [Use Application Insights with Azure Diagnostics tootroubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="93ff4-117">hello **채널** 요소 하나 이상 포함 **채널** 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-117">hello **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="93ff4-118">hello *이름* 특성 toothat 채널을 고유 하 게 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-118">hello *name* attribute uniquely refers toothat channel.</span></span>
    - <span data-ttu-id="93ff4-119">hello *loglevel* 특성 채널 hello hello 로그 수준 수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-119">hello *loglevel* attribute lets you specify hello log level that hello channel allows.</span></span> <span data-ttu-id="93ff4-120">대부분 tooleast 정보의 순서로 hello 사용 가능한 로그 수준은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-120">hello available log levels in order of most tooleast information are:</span></span>
        - <span data-ttu-id="93ff4-121">자세한 정보 표시</span><span class="sxs-lookup"><span data-stu-id="93ff4-121">Verbose</span></span>
        - <span data-ttu-id="93ff4-122">정보</span><span class="sxs-lookup"><span data-stu-id="93ff4-122">Information</span></span>
        - <span data-ttu-id="93ff4-123">Warning</span><span class="sxs-lookup"><span data-stu-id="93ff4-123">Warning</span></span>
        - <span data-ttu-id="93ff4-124">오류</span><span class="sxs-lookup"><span data-stu-id="93ff4-124">Error</span></span>
        - <span data-ttu-id="93ff4-125">중요</span><span class="sxs-lookup"><span data-stu-id="93ff4-125">Critical</span></span>

<span data-ttu-id="93ff4-126">채널 필터 처럼 작동 하 고 tooselect 특정 로그 수준 toosend toohello 대상 싱크 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-126">A channel acts like a filter and allows you tooselect specific log levels toosend toohello target sink.</span></span> <span data-ttu-id="93ff4-127">예를 들어 자세한 로그를 수집 하 고 toostorage, 보낼 하지만 오류 toohello 싱크만 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-127">For example, you could collect verbose logs and send them toostorage, but send only Errors toohello sink.</span></span>

<span data-ttu-id="93ff4-128">hello 다음 그래픽에서는이 관계</span><span class="sxs-lookup"><span data-stu-id="93ff4-128">hello following graphic shows this relationship.</span></span>

![진단 공용 구성](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="93ff4-130">다음 그래픽 hello hello 구성 값 및 작동 방법을 요약 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-130">hello following graphic summarizes hello configuration values and how they work.</span></span> <span data-ttu-id="93ff4-131">Hello 구성 hello 계층 구조의 여러 수준에서 여러 개의 싱크를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-131">You can include multiple sinks in hello configuration at different levels in hello hierarchy.</span></span> <span data-ttu-id="93ff4-132">hello 싱크 hello 최상위에 역할 전역 설정 하며 hello 하나에서 지정 된 개별 hello 요소 재정의 toothat 전역 설정을 처럼 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-132">hello sink at hello top level acts as a global setting and hello one specified at hello individual element acts like an override toothat global setting.</span></span>

![Application Insights를 사용한 진단 싱크 구성](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="93ff4-134">전체 싱크 구성 예제</span><span class="sxs-lookup"><span data-stu-id="93ff4-134">Complete sink configuration example</span></span>
<span data-ttu-id="93ff4-135">전체 예제는 hello 공용 구성 파일을 다음과 같습니다</span><span class="sxs-lookup"><span data-stu-id="93ff4-135">Here is a complete example of hello public configuration file that</span></span>
1. <span data-ttu-id="93ff4-136">모든 오류 tooApplication Insights 보냅니다 (hello에서 지정 된 **DiagnosticMonitorConfiguration** 노드)</span><span class="sxs-lookup"><span data-stu-id="93ff4-136">sends all errors tooApplication Insights (specified at hello **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="93ff4-137">또한 hello 응용 프로그램 로그에 대 한 자세한 정보 표시 수준 로그를 보냅니다 (hello에서 지정 된 **로그** 노드).</span><span class="sxs-lookup"><span data-stu-id="93ff4-137">also sends Verbose level logs for hello Application Logs (specified at hello **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent toothis channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent toothis channel -->
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
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent toothis channel",
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
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent toothis channel"
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
<span data-ttu-id="93ff4-138">Hello 이전 구성 위의 삼각형 hello hello 의미에 따라 지정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-138">In hello previous configuration, hello following lines have hello following meanings:</span></span>

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="93ff4-139">Azure 진단으로 수집 하는 모든 hello 데이터 보내기</span><span class="sxs-lookup"><span data-stu-id="93ff4-139">Send all hello data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a><span data-ttu-id="93ff4-140">만 오류 로그 toohello Application Insights 싱크가 보내기</span><span class="sxs-lookup"><span data-stu-id="93ff4-140">Send only error logs toohello Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a><span data-ttu-id="93ff4-141">자세한 정보 응용 프로그램 로그 tooApplication Insights 보내기</span><span class="sxs-lookup"><span data-stu-id="93ff4-141">Send Verbose application logs tooApplication Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="93ff4-142">제한 사항</span><span class="sxs-lookup"><span data-stu-id="93ff4-142">Limitations</span></span>

- <span data-ttu-id="93ff4-143">**성능 카운터가 아닌 로그 유형인 채널**</span><span class="sxs-lookup"><span data-stu-id="93ff4-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="93ff4-144">성능 카운터 요소를 사용하여 채널을 지정하는 경우 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="93ff4-145">**채널에 대 한 로그 수준을 hello Azure 진단으로 수집 되 고 hello 로그 수준을 초과할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="93ff4-145">**hello log level for a channel cannot exceed hello log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="93ff4-146">예를 들어 hello 로그 요소에 대 한 응용 프로그램 로그 오류를 수집할 수 없으며 toosend 자세한 로그 toohello Application Insight 싱크를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="93ff4-146">For example, you cannot collect Application Log errors in hello Logs element and try toosend Verbose logs toohello Application Insight sink.</span></span> <span data-ttu-id="93ff4-147">hello *scheduledTransferLogLevelFilter* 특성 항상 수집 하 여 동일 하 고 있거나 hello 로그 보다 더 많은 로그 toosend tooa 싱크 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-147">hello *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than hello logs you are trying toosend tooa sink.</span></span>
- <span data-ttu-id="93ff4-148">**Azure 진단 확장 tooApplication Insights에 의해 수집 된 blob 데이터를 보낼 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="93ff4-148">**You cannot send blob data collected by Azure diagnostics extension tooApplication Insights.**</span></span> <span data-ttu-id="93ff4-149">예를 들어 hello 아래에 지정 된 아무것도 *디렉터리* 노드.</span><span class="sxs-lookup"><span data-stu-id="93ff4-149">For example, anything specified under hello *Directories* node.</span></span> <span data-ttu-id="93ff4-150">크래시 덤프 hello 실제 크래시 덤프 전송 tooblob 저장소 및 크래시 덤프 hello 알림만 생성 된 tooApplication Insights 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-150">For Crash Dumps hello actual crash dump is sent tooblob storage and only a notification that hello crash dump was generated is sent tooApplication Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93ff4-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="93ff4-151">Next Steps</span></span>
* <span data-ttu-id="93ff4-152">너무 방법에 대해 알아봅니다[Azure 진단 정보를 볼](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) Application Insights에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-152">Learn how too[view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="93ff4-153">사용 하 여 [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello 응용 프로그램에 대 한 Azure 진단 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="93ff4-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="93ff4-154">사용 하 여 [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello 응용 프로그램에 대 한 Azure 진단 확장</span><span class="sxs-lookup"><span data-stu-id="93ff4-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello Azure diagnostics extension for your application</span></span>
