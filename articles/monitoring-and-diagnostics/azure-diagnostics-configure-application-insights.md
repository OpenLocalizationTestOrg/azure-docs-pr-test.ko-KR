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
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-tooapplication-insights"></a>클라우드 서비스, 가상 컴퓨터 또는 서비스 패브릭 진단 데이터 tooApplication Insights 보내기
가상 컴퓨터, 가상 컴퓨터 크기 집합 및 서비스 패브릭 모든 클라우드 서비스는 hello Azure 진단 확장 toocollect 데이터를 사용합니다.  Azure 진단 데이터 tooAzure 저장소 테이블을 보냅니다.  그러나 수도 있습니다 모든 파이프 또는 Azure 진단 확장 1.5 이상을 사용 하 여 hello 데이터 tooother 위치의 하위 집합입니다.

이 문서에서는 toosend 데이터를 Azure 진단 확장 tooApplication Insights hello 하는 방법을 설명 합니다.

## <a name="diagnostics-configuration-explained"></a>설명한 진단 구성
진단 데이터를 보낼 수 있는 추가 위치는 Azure 진단 확장 1.5 도입 된 싱크를 hello 합니다.

Application Insights에 대한 싱크 예제 구성:

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
- hello **싱크** *이름* 특성은 hello 싱크를 고유 하 게 식별 하는 문자열 값입니다.

- hello **ApplicationInsights** 요소 hello hello Azure 진단 데이터를 보내는 위치 Application insights 리소스의 계측 키를 지정 합니다.
    - 기존 Application Insights 리소스를 설정 하지 않은 경우 참조 [새 Application Insights 리소스 만들기](../application-insights/app-insights-create-new-resource.md) 리소스 만들기 및 hello 계측 키 가져오기에 대 한 자세한 내용은 합니다.
    - Azure SDK 2.8 이상에서 클라우드 서비스를 개발하는 경우 이 계측 키는 자동으로 채워집니다. hello 값은 hello 기반 **APPINSIGHTS_INSTRUMENTATIONKEY** hello 클라우드 서비스 프로젝트를 패키지할 때 서비스 구성 설정입니다. 참조 [Azure 진단 tootroubleshoot 있는 Application Insights를 사용 하 여 클라우드 서비스는 발급](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md)합니다.

- hello **채널** 요소 하나 이상 포함 **채널** 요소입니다.
    - hello *이름* 특성 toothat 채널을 고유 하 게 참조 합니다.
    - hello *loglevel* 특성 채널 hello hello 로그 수준 수를 지정할 수 있습니다. 대부분 tooleast 정보의 순서로 hello 사용 가능한 로그 수준은 다음과 같습니다.
        - 자세한 정보 표시
        - 정보
        - Warning
        - 오류
        - 중요

채널 필터 처럼 작동 하 고 tooselect 특정 로그 수준 toosend toohello 대상 싱크 있습니다. 예를 들어 자세한 로그를 수집 하 고 toostorage, 보낼 하지만 오류 toohello 싱크만 보낼 수 있습니다.

hello 다음 그래픽에서는이 관계

![진단 공용 구성](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

다음 그래픽 hello hello 구성 값 및 작동 방법을 요약 합니다. Hello 구성 hello 계층 구조의 여러 수준에서 여러 개의 싱크를 포함할 수 있습니다. hello 싱크 hello 최상위에 역할 전역 설정 하며 hello 하나에서 지정 된 개별 hello 요소 재정의 toothat 전역 설정을 처럼 작동 합니다.

![Application Insights를 사용한 진단 싱크 구성](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a>전체 싱크 구성 예제
전체 예제는 hello 공용 구성 파일을 다음과 같습니다
1. 모든 오류 tooApplication Insights 보냅니다 (hello에서 지정 된 **DiagnosticMonitorConfiguration** 노드)
2. 또한 hello 응용 프로그램 로그에 대 한 자세한 정보 표시 수준 로그를 보냅니다 (hello에서 지정 된 **로그** 노드).

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
Hello 이전 구성 위의 삼각형 hello hello 의미에 따라 지정 되어 있습니다.

### <a name="send-all-hello-data-that-is-being-collected-by-azure-diagnostics"></a>Azure 진단으로 수집 하는 모든 hello 데이터 보내기

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-toohello-application-insights-sink"></a>만 오류 로그 toohello Application Insights 싱크가 보내기

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-tooapplication-insights"></a>자세한 정보 응용 프로그램 로그 tooApplication Insights 보내기

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a>제한 사항

- **성능 카운터가 아닌 로그 유형인 채널** 성능 카운터 요소를 사용하여 채널을 지정하는 경우 무시됩니다.
- **채널에 대 한 로그 수준을 hello Azure 진단으로 수집 되 고 hello 로그 수준을 초과할 수 없습니다.** 예를 들어 hello 로그 요소에 대 한 응용 프로그램 로그 오류를 수집할 수 없으며 toosend 자세한 로그 toohello Application Insight 싱크를 시도 하십시오. hello *scheduledTransferLogLevelFilter* 특성 항상 수집 하 여 동일 하 고 있거나 hello 로그 보다 더 많은 로그 toosend tooa 싱크 합니다.
- **Azure 진단 확장 tooApplication Insights에 의해 수집 된 blob 데이터를 보낼 수 없습니다.** 예를 들어 hello 아래에 지정 된 아무것도 *디렉터리* 노드. 크래시 덤프 hello 실제 크래시 덤프 전송 tooblob 저장소 및 크래시 덤프 hello 알림만 생성 된 tooApplication Insights 전송 됩니다.

## <a name="next-steps"></a>다음 단계
* 너무 방법에 대해 알아봅니다[Azure 진단 정보를 볼](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) Application Insights에서 합니다.
* 사용 하 여 [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) tooenable hello 응용 프로그램에 대 한 Azure 진단 확장 합니다.
* 사용 하 여 [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) tooenable hello 응용 프로그램에 대 한 Azure 진단 확장
