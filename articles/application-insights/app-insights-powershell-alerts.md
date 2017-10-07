---
title: "Application Insights에서 aaaUse Powershell tooset 경고 | Microsoft Docs"
description: "메트릭 변경에 대 한 Application Insights tooget 전자 메일의 구성을 자동화 합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a>Application Insights에서 PowerShell tooset 경고를 사용 합니다.
hello 구성을 자동화할 수 있습니다 [경고](app-insights-alerts.md) 에 [Application Insights](app-insights-overview.md)합니다.

수 또한 [webhook tooautomate 응답 tooan 경고를 설정](../monitoring-and-diagnostics/insights-webhooks-alerts.md)합니다.

> [!NOTE]
> Toocreate 리소스과 경고를 원하는 경우 hello 동일한 시간을 고려 하십시오 [Azure 리소스 관리자 템플릿을 사용 하 여](app-insights-powershell.md)합니다.
>
>

## <a name="one-time-setup"></a>일 회 설정
아직 Azure 구독에서 PowerShell을 사용한 적이 없을 경우:

Toorun hello 스크립트 저장할 hello 머신에서 hello Azure Powershell 모듈을 설치 합니다.

* [Microsoft 웹 플랫폼 설치 관리자(v5 이상)](http://www.microsoft.com/web/downloads/platform.aspx)를 설치합니다.
* Microsoft Azure Powershell tooinstall 사용

## <a name="connect-tooazure"></a>TooAzure 연결
Azure PowerShell을 시작 하 고 [tooyour 구독 연결](/powershell/azure/overview):

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a>경고 받기
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a>경고 추가
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a>예 1
(5 분) 평균 hello 서버 응답 tooHTTP 요청 1 초 보다 느린 경우 내게 메일 보내기. Application Insights 리소스의 이름이 IceCreamWebApp이며 리소스 그룹 Fabrikam 내에 있습니다. 저는 hello 소유자 hello Azure 구독입니다.

hello GUID hello 구독 ID (hello 계측 키가 아니라 hello 응용 프로그램의)입니다.

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a>예 2
응용 프로그램을 사용 중인 [trackmetric ()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport "salesPerHour." 라는 메트릭 평균을 24 시간 이상 100 개 이하로 떨어지면 "salesPerHour" 전자 메일 toomy 동료를 보냅니다.

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

hello 메트릭에 대 한 동일한 규칙을 사용할 수는 hello hello를 사용 하 여 보고할 [측정 매개 변수](app-insights-api-custom-events-metrics.md#properties) TrackEvent trackPageView 등 다른 추적 호출 합니다.

## <a name="metric-names"></a>메트릭 이름
| 메트릭 이름 | 화면 이름 | 설명 |
| --- | --- | --- |
| `basicExceptionBrowser.count` |브라우저 예외 |Hello 브라우저에서 발생 한 예외를 확인할 수 없는 횟수입니다. |
| `basicExceptionServer.count` |서버 예외 |Hello 응용 프로그램에서 throw 된 처리 되지 않은 예외 수 |
| `clientPerformance.clientProcess.value` |클라이언트 처리 시간 |Hello DOM 로드 될 때까지 hello 문서의 마지막 바이트 받기 사이의 시간입니다. 비동기 요청은 계속 처리 중일 수 있습니다. |
| `clientPerformance.networkConnection.value` |페이지 로드 네트워크 연결 시간 |시간 hello 브라우저 tooconnect toohello 네트워크를 사용합니다. 캐시된 경우 0일 수 있습니다. |
| `clientPerformance.receiveRequest.value` |응답 수신 시간 |브라우저 요청 toostarting tooreceive 응답을 보내는 사이의 시간입니다. |
| `clientPerformance.sendRequest.value` |요청 전송 시간 |브라우저 toosend 요청에서 사용한 시간입니다. |
| `clientPerformance.total.value` |브라우저 페이지 로드 시간 |사용자가 요청한 때부터 DOM, 스타일시트, 스크립트 및 이미지가 로드될 때까지 소요된 시간입니다. |
| `performanceCounter.available_bytes.value` |사용 가능한 메모리 |처리를 위해서나 시스템에서 바로 사용할 수 있는 실제 메모리입니다. |
| `performanceCounter.io_data_bytes_per_sec.value` |프로세스 IO 속도 |두 번째 읽기 및 서 면된 toofiles, 네트워크 및 장치 당 총 바이트 수입니다. |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |예외 속도 |초당 발생한 예외입니다. |
| `performanceCounter.percentage_processor_time.value` |CPU 프로세스 |hello 응용 프로그램 프로세스에 대 한 hello 프로세서 tooexecution 명령에서 사용 되는 모든 프로세스 스레드의 경과 된 시간의 hello 비율입니다. |
| `performanceCounter.percentage_processor_total.value` |프로세서 시간 |비 유휴 스레드를에서 소비한 hello 백분율 hello 프로세서 시간입니다. |
| `performanceCounter.process_private_bytes.value` |프로세스 전용 바이트 |만 toohello 할당 된 메모리는 응용 프로그램의 프로세스를 모니터링 합니다. |
| `performanceCounter.request_execution_time.value` |ASP.NET 요청 실행 시간 |Hello 가장 최근 요청의 실행 시간입니다. |
| `performanceCounter.requests_in_application_queue.value` |실행 큐의 ASP.NET 요청 |Hello 응용 프로그램 요청 큐의 길이입니다. |
| `performanceCounter.requests_per_sec.value` |ASP.NET 요청 속도 |모든 속도 ASP.NET에서 초당 toohello 응용 프로그램을 요청합니다. |
| `remoteDependencyFailed.durationMetric.count` |종속성 실패 |실패 한 hello 서버 응용 프로그램 tooexternal 리소스별 호출의 수입니다. |
| `request.duration` |서버 응답 시간 |HTTP 요청 받기와 hello 응답 보내기 완료 사이의 시간입니다. |
| `request.rate` |요청 속도 |초당 toohello 응용 프로그램을 요청 하는 모든의 비율입니다. |
| `requestFailed.count` |실패한 요청 |응답 코드가 400 이상인 HTTP 요청의 개수입니다. |
| `view.count` |페이지 보기 |웹 페이지에 대한 클라이언트 사용자 요청의 수입니다. 가상 트래픽은 필터링됩니다. |
| {사용자 지정 메트릭 이름} |{사용자의 메트릭 이름} |사용자가 메트릭 값에서 보고 [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) 또는 hello [추적 호출의 매개 변수 측정](app-insights-api-custom-events-metrics.md#properties)합니다. |

hello 메트릭 여러 원격 모듈에 의해 보내집니다.

| 메트릭 그룹 | 수집기 모듈 |
| --- | --- |
| basicExceptionBrowser,<br/>clientPerformance,<br/>view |[브라우저 JavaScript](app-insights-javascript.md) |
| performanceCounter |[성능](app-insights-configuration-with-applicationinsights-config.md) |
| remoteDependencyFailed |[종속성](app-insights-configuration-with-applicationinsights-config.md) |
| request,<br/>requestFailed |[서버 요청](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a>Webhook
있습니다 수 [응답 tooan 경고 자동화](../monitoring-and-diagnostics/insights-webhooks-alerts.md)합니다. 경고가 발생한 경우 Azure에서 사용자가 선택한 웹 주소를 호출합니다.

## <a name="see-also"></a>참고 항목
* [스크립트 tooconfigure Application Insights](app-insights-powershell-script-create-resource.md)
* [서식 파일에서 Application Insights 및 웹 테스트 리소스 만들기](app-insights-powershell.md)
* [Microsoft Azure 진단 tooApplication Insights 결합 자동화](app-insights-powershell-azure-diagnostics.md)
* [응답 tooan 경고 자동화](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
