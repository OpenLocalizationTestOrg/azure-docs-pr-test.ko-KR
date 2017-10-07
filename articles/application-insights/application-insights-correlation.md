---
title: "응용 프로그램 Insights 원격 분석 상관 관계 aaaAzure | Microsoft Docs"
description: "Application Insights 원격 분석 상관 관계"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Application Insights의 원격 분석 상관 관계

마이크로 서비스의 hello world, 모든 논리 작업에는 hello 서비스의 다양 한 구성 요소에서 작업을 수행 해야 합니다. 이러한 각 구성 요소는 [Application Insights](app-insights-overview.md)에서 개별적으로 모니터링할 수 있습니다. hello 웹 응용 프로그램 구성 요소에는 시각화에 대 한 hello API 구성 요소 tooget 데이터 및 인증 공급자 구성 요소 toovalidate 사용자 자격 증명을와 통신 합니다. 차례로 hello API 구성 요소 캐시 공급자 구성 요소를 사용 및 알림 hello 청구 구성 요소에서이 통화에 대 한 다른 서비스에서 데이터를 쿼리할 수 있습니다. Application Insights는 분산 원격 분석 상관 관계를 지원합니다. 어떤 구성 요소는 성능 저하 또는 실패에 대 한 toodetect이 있습니다.

이 문서는 여러 구성 요소에서 보낸 Application Insights toocorrelate 원격 분석에서 사용 하는 hello 데이터 모델을 설명 합니다. Hello 컨텍스트 전파 기술 및 프로토콜을 포함합니다. 또한 hello 구현을 서로 다른 언어 및 플랫폼에 hello 상관 관계 개념을 다룹니다.

## <a name="telemetry-correlation-data-model"></a>원격 분석 상관 관계 데이터 모델

Application Insights는 분산 원격 분석 상관 관계에 대한 [데이터 모델](application-insights-data-model.md)을 정의합니다. 원격 분석 tooassociate hello 논리 작업과 모든 원격 분석 항목에 라는 컨텍스트 필드가 `operation_Id`합니다. 이 식별자는 분산 hello 추적에서 모든 원격 분석 항목에서 공유 됩니다. 따라서 단일 계층에서 원격 분석이 손실되더라도 다른 구성 요소에서 보고한 원격 분석을 연결할 수 있습니다.

분산된 논리 연산 집합 더 작은 작업-hello 구성 요소 중 하나에서 처리 요청을 일반적으로 구성 됩니다. 이러한 작업은 [요청 원격 분석](application-insights-data-model-request-telemetry.md)을 통해 정의됩니다. 모든 요청 원격 분석에는 전체적으로 고유하게 식별되는 자체 `id`가 있습니다. 모든 원격 분석-추적, 예외 등이 요청과 관련 된 hello 설정할 `operation_parentId` toohello 요청 값의 hello `id`합니다.

모든 송신 작업 예: http 호출 tooanother 구성 요소를 나타내는 [종속성 원격 분석](application-insights-data-model-dependency-telemetry.md)합니다. 종속성 원격 분석은 전체적으로 고유한 자체 `id`도 정의합니다. 이 종속성 호출을 통해 시작된 요청 원격 분석은 이를 `operation_parentId`로 사용합니다.

Hello 보기의 분산된 논리 연산을 사용 하 여 빌드할 수 `operation_Id`, `operation_parentId`, 및 `request.id` 와 `dependency.id`합니다. 이러한 필드는 또한 원격 분석 호출 hello 인과 관계 순서를 정의합니다.

마이크로 서비스 환경에서 구성 요소에서 추적 toohello 다른 저장소를 진행할 수 있습니다. 모든 구성 요소는 Application Insights에 자체 계측 키가 있을 수 있습니다. 원격 분석 tooget hello 논리 연산에 대 한 모든 저장소 tooquery 데이터가 필요 합니다. 위치에서 toohave 힌트가 필요한 수의 저장소 이면 거 대 한 toolook 다음 합니다.

Application Insights 데이터 모델 두 개를 정의 합니다.이 문제를 toosolve 필드: `request.source` 및 `dependency.target`합니다. 첫 번째 필드에 hello hello 종속성 요청을 시작한 hello 구성 요소를 식별 하 고 hello에는 두 번째 hello 종속성 호출의 hello 응답이 반환 되었습니다. 구성 요소를 식별 합니다.


## <a name="example"></a>예제

Hello 현재 시장 가격 주식 API를 호출 하는 hello 외부 API를 사용 하는 주가 표시 하는 응용 프로그램 주식 가격의 예를 들어를 보겠습니다. hello 주식 가격 응용 프로그램에는 페이지가 `Stock page` hello 클라이언트 웹 브라우저를 사용 하 여 열린 `GET /Home/Stock`합니다. hello 응용 프로그램 쿼리 HTTP 호출을 사용 하 여 재고 API hello `GET /api/stock/value`합니다.

쿼리를 실행하여 결과 원격 분석을 분석할 수 있습니다.

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

모든 원격 분석 항목 hello 루트를 공유 하는 hello 결과 보기 note에서 `operation_Id`합니다. Hello 페이지-새로운 고유 id에서에서 만든 ajax 호출 하는 경우 `qJSXU` 할당된 toohello 종속성 원격 분석은 및 페이지 보기의 id로 사용 됩니다 `operation_ParentId`합니다. 따라서 서버 요청은 Ajax의 ID를 `operation_ParentId`로 사용합니다.

| itemType   | name                      | id           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Stock page                |              | STYz               | STYz         |
| dependency | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| request    | GET Home/Stock            | KqKwlrSt9PA= | qJSXU              | STYz         |
| dependency | GET /api/stock/value      | bBrf2L7mm2g= | KqKwlrSt9PA=       | STYz         |

이제 호출 때 hello `GET /api/stock/value` 해당 서버의 tooknow hello id 원하는 tooan 외부 서비스를 수행 합니다. 따라서 `dependency.target` 필드를 적절하게 설정할 수 있습니다. Hello 외부 서비스-모니터링을 지원 하지 않을 때 `target` 같은 hello 서비스의 호스트 이름을 toohello 설정 되어 `stock-prices-api.com`합니다. 그러나 해당 서비스는 미리 정의 된 반환 하 여 자신을 식별 하는 경우 HTTP 헤더- `target` 해당 서비스의 원격 분석을 쿼리하여 Application Insights distributed toobuild 추적을 허용 하는 hello 서비스 id를 포함 합니다. 

## <a name="correlation-headers"></a>상관 관계 헤더

Hello에 대 한 RFC 제안 작업 [HTTP 프로토콜 상관 관계](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md)합니다. 이 제안은 다음 두 가지 헤더를 정의합니다.

- `Request-Id`hello 호출의 hello 전역적으로 고유 id를 전달 합니다.
- `Correlation-Context`-hello distributed hello 추적 속성의 이름 값 쌍 컬렉션을 수행 합니다.

hello 표준의 두 개의 스키마 정의 `Request-Id` 세대-플랫 및 계층적입니다. Hello 플랫 스키마는 잘 알려진 `Id` hello에 대해 정의 된 키 `Correlation-Context` 컬렉션입니다.

Application Insights 정의 hello [확장](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) hello 상관 관계 HTTP 프로토콜에 대 한 합니다. 사용 하 여 `Request-Context` toopropagate hello 컬렉션 hello 직접 실행 호출자 또는 호출 수신자에 의해 사용 되는 속성의 이름-값 쌍입니다. Application Insights SDK 사용이 헤더 tooset `dependency.target` 및 `request.source` 필드입니다.

## <a name="open-tracing-and-application-insights"></a>Open Tracing 및 Application Insights

[Open Tracing](http://opentracing.io/) 및 Application Insights 데이터 모델은 다음과 같이 표시됩니다. 

- `request``pageView` 너무 매핑합니다**범위** 와`span.kind = server`
- `dependency`너무 매핑합니다**범위** 와`span.kind = client`
- `id``request` 및 `dependency` 너무 매핑합니다**Span.Id**
- `operation_Id`너무 매핑합니다**traceid가**
- `operation_ParentId`너무 매핑합니다**참조** 형식의`ChileOf`

Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.

Open Tracing 개념의 정의는 [specification](https://github.com/opentracing/specification/blob/master/specification.md)(사양) 및 [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md)를 참조하세요.


## <a name="telemetry-correlation-in-net"></a>.NET의 원격 분석 상관 관계

시간이 지남에 따라.NET 정의 다양 한 방법으로 toocorrelate 원격 분석 및 진단 로그 합니다. `System.Diagnostics.CorrelationManager` tootrack 허용 [LogicalOperationStack 및 ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx)합니다. `System.Diagnostics.Tracing.EventSource`ETW Windows hello 메서드를 정의 하 고 [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx)합니다. `ILogger`는 [Log Scopes](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes)(로그 범위)를 사용합니다. WCF 및 HTTP는 "현재" 컨텍스트 전파를 연결합니다.

하지만 해당 메서드는 자동 분산 추적 지원을 사용하지 않았습니다. `DiagnosticsSource`컴퓨터 상관 관계 교차 자동 방식으로 toosupport 수행 됩니다. .NET 라이브러리는 진단 소스를 지원 하 고 http 같은 hello 전송을 통해 hello 상관 관계 컨텍스트의 자동 컴퓨터 간 전파를 허용 합니다.

hello [tooActivities 안내](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) 진단 소스 활동 추적의 hello 기본 사항을 설명 합니다. 

새 활동 hello 시작 및 ASP.NET 코어 2.0 지원 Http 헤더를 추출 합니다. 

`System.Net.HttpClient`시작 버전 `<fill in>` hello 상관 관계 Http 헤더 및 활동으로 hello http 호출 추적의 자동 삽입을 지원 합니다.

새 Http 모듈 [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) ASP.NET 클래식 hello에 대 한 합니다. 이 모듈은 DiagnosticsSource를 사용하여 원격 분석 상관 관계를 구현합니다. 들어오는 요청 헤더를 기반으로 활동을 시작합니다. 또한 hello 요청 처리의 여러 단계에서 원격 분석을 연관 시킵니다. Hello 경우 IIS 처리의 모든 단계는 다른 관리 스레드에서 실행 될 때에

응용 프로그램 Insights SDK 시작 버전 `2.4.0-beta1` DiagnosticsSource 및 활동 toocollect 원격 분석을 사용 하 고 hello 현재 활동에 연결 합니다. 

## <a name="next-steps"></a>다음 단계

- [사용자 지정 원격 분석을 작성합니다](app-insights-api-custom-events-metrics.md).
- Application Insights에서 마이크로 서비스의 모든 구성 요소를 등록합니다. [지원되는 플랫폼](app-insights-platforms.md)을 확인합니다.
- Application Insights 형식 및 데이터 모델에 대한 자세한 내용은 [데이터 모델](application-insights-data-model.md)을 참조하세요.
- 너무 방법에 대해 알아봅니다[확장 하 고 원격 분석 필터링](app-insights-api-filtering-sampling.md)합니다.
