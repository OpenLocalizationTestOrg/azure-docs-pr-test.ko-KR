---
title: "웹 앱 aaaMonitor | Microsoft Docs"
description: "자세한 방법을 tooset 웹 앱에 대 한 모니터링 구성"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>App Service 모니터링
이 자습서에서는 응용 프로그램을 모니터링 하 고 발생 하는 경우 기본 제공 플랫폼 도구 toosolve 문제가 hello를 사용 하 여 안내 합니다.

이 문서의 각 섹션은 특정 기능을 설명합니다. Hello 기능을 함께 사용 하는 수 있습니다.
- 앱 문제 식별
- Hello 문제는 코드 또는 hello 플랫폼 인해 발생 하는 시기를 결정 합니다.
- Hello 소스 코드에서 hello 문제의 범위를 좁힙니다.
- 디버깅 하 고 hello 문제를 수정 합니다.

## <a name="before-you-begin"></a>시작하기 전에
- 웹 앱 toomonitor 필요 하 고 hello에 따라 단계를 설명 합니다.
    - Hello에 설명 된 hello 단계 후 응용 프로그램을 만들 수 있습니다 [SQL 데이터베이스를 사용 하 여 Azure에 ASP.NET 응용 프로그램을 만들](app-service-web-tutorial-dotnet-sqldatabase.md) 자습서입니다.

- Tootry 하려는 경우 **원격 디버깅** Visual Studio 응용 프로그램의 필요 합니다.
    - 설치 된 Visual Studio 2017 없는 경우 다운로드 하 고 무료 hello를 사용 하 여 수 [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)합니다.
    - 사용할 수 있는지 확인 **Azure 개발** hello Visual Studio 설정 중입니다.

## <a name="metrics"></a> 1단계 - 메트릭 보기
**메트릭** 유용한 toounderstand 됩니다.
- 응용 프로그램 상태
- 앱 성능
- 리소스 사용

응용 프로그램 문제를 조사할 때 좋은 위치 toostart은 메트릭을 검토 합니다. Azure 포털에 검사를 사용 하 여 응용 프로그램의 hello 메트릭을 신속 하 게 toovisually **Azure 모니터**합니다.

메트릭은 앱의 여러 주요 집계에 대한 기록 보기를 제공합니다. 앱 서비스에서 호스팅되는 모든 앱에 대 한 웹 앱 hello와 hello 앱 서비스 계획 모니터링 해야 합니다.

> [!NOTE]
> 앱 서비스 계획 사용 하는 실제 리소스 toohost의 hello 컬렉션 응용을 프로그램을 나타냅니다. 앱 서비스 계획 공유 hello 리소스 toosave 비용 허용 여러 앱을 호스트 하는 경우에서 정의한 tooan 할당 하는 모든 응용 프로그램입니다.
>
> App Service 계획은 다음을 정의합니다.
> * 지역: 북유럽, 미국 동부, 동남 아시아 등
> * 인스턴스 크기: 소, 중, 대 등
> * 확장 개수: 1, 2, 3개 인스턴스 등
> * SKU: 무료, 공유, 기본, 표준, 프리미엄 등

이동 toohello 웹 응용 프로그램에 대 한 메트릭을 tooreview **개요** 블레이드 toomonitor hello 응용 프로그램의 원하는 합니다. 여기에서 앱의 메트릭에 대한 차트를 **모니터링 타일**로 볼 수 있습니다. Hello 타일 tooedit 클릭 어떤 메트릭 tooview를 구성 하 고 시간 범위 toodisplay hello 합니다.

기본 hello 리소스 블레이드도 hello 응용 프로그램 요청에 대 한 뷰 및 지난 1 시간 동안 hello에 대 한 오류를 제공합니다.
![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

많은 생성 하는 응용 프로그램이 있다고 hello 예에서 보시 **HTTP 서버 오류**합니다. hello 많은 양의 오류 표시가 hello 첫 번째 tooinvestigate이 응용이 프로그램 필요 합니다.

> [!TIP]
> 자세한 정보 Azure 모니터에 대 한 링크를 따라 hello로:
> - [Azure Monitor 시작](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Azure 메트릭](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Azure Monitor에서 지원되는 메트릭](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Azure 대시보드](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a> 2단계 - 경고 구성
**경고** 앱에 대 한 특정 조건에 구성 된 tootrigger 될 수 있습니다.

[1 단계-메트릭 확인할](#metrics), hello 응용 프로그램에 오류 수가 있는지에 대해 살펴보았습니다.

경고를 구성할 수 있습니다. tooautomatically 오류가 발생 하는 경우 알림을 받습니다. 이 경우 원하는 hello 경고 toosend 하 고 hello HTTP 50 X 오류 수가 특정 임계값을 초과 될 때마다 전자 메일.

경고, toocreate 너무 이동**모니터링** > **경고** 클릭 **[+], 추가 경고**합니다.

![경고](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Hello 경고 구성에 대 한 값을 제공 합니다.
- **리소스:** hello 경고와 사이트 toomonitor hello 합니다.
- **이름:** 경고의 이름입니다(이 경우 *High HTTP 50X*).
- **설명:** 이 경고에 대한 일반 텍스트 설명입니다.
- **경고 대상:** 경고 대상은 메트릭 또는 이벤트(이 예제에서는 메트릭)가 될 수 있습니다.
- **메트릭:** 이 경우 어떤 메트릭 toomonitor: *HTTP 서버 오류*합니다.
- **조건:** tooalert,이 경우 select hello *보다 큰* 옵션입니다.
- **임계값:** 이 경우,에 대 한 값 toolook 사용 이란: *400*합니다.
- **기간:** 경고 hello는 메트릭의 평균 값을 통해 작동 합니다. 시간이 짧을수록 민감한 경고가 발생합니다. 이 경우 *5분*입니다.
- **메일 소유자 및 참가자:** 이 예에서는 *사용*입니다.

Hello 경고가 만들어지고 전자 메일 했으므로 hello 앱 라인 hello 구성 된 임계값 초과 될 때마다 전송 됩니다. Hello Azure 포털에서에서 활성 경고를 검토할 수도 있습니다.

![트리거된 경고](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> 자세한 정보 Azure 경고에 대 한 링크를 따라 hello로:
> - [Microsoft Azure의 경고란?](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [메트릭에 대한 작업](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [메트릭 경고 만들기](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a> 3단계 - App Service 도우미
**앱 서비스 도우미** 편리 toomonitor 하면 모바일 장치 (iOS 또는 Android)에서 네이티브 환경 사용 하 여 앱을 제공 합니다.

App Service 도우미를 사용하여 다음을 수행합니다.
- 응용 프로그램 메트릭 검토
- 경고 및 권장 사항 검토 및 조치
- 기본적인 문제 해결 (찾아보기, 시작, 중지, 다시 시작 hello 앱)를 수행 합니다.
- 중요한 이벤트에 대한 푸시 알림을 가져옵니다.

![App Service 도우미](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![App Service 도우미 App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service 도우미 Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

앱 서비스 도우미 hello에서 설치할 수 있습니다 [앱 스토어](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) 또는 [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a> 4단계 - 문제 진단 및 해결
**문제 진단 및 해결**은 플랫폼 문제와 응용 프로그램 문제를 구분할 수 있도록 도와 줍니다. 웹 앱 백 toohealthy 완화할 수 있는 방법은 tooget를 제안할 수도 것입니다.

![문제 진단 및 해결](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Hello 예제 양식 이전 단계를 계속 볼 수 있습니다는 hello 응용 프로그램에 되었습니다 여 고가용성 때 문제가 발생 합니다. 반면, hello 사용 가능한 플랫폼 100%에서 이동 되지 있습니다.

때 hello 앱은 문제가 아니며 hello를 플랫폼 유지 되며, 응용 프로그램 문제에 대해 처리 중인 뚜렷한 합니다.

## <a name="logging"></a>5 단계 - 로깅
Hello 오류 tooan 응용 프로그램 문제를 축소 한 우리, 했으므로 자세한 내용은 hello 응용 프로그램 및 서버 로그 tooget에서 찾을 수 있습니다.

로깅을 통해 toocollect 두 **Application Diagnostics** 및 **웹 서버 진단** 웹 앱에 대 한 로그입니다.

### <a name="application-diagnostics"></a>응용 프로그램 진단
응용 프로그램 진단 있습니다 toocapture에서 생성 한 추적 런타임 시 hello 응용 프로그램을 허용 합니다.

추가 추적 tooyour 응용 프로그램 크게 향상 기능 toodebug 및-고정점 문제.

Asp.net에서 사용 하 여 응용 프로그램 추적을 기록할 수 있습니다 [System.Diagnostics.Trace 클래스](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) hello 로그 인프라에서 캡처되는 toogenerate 이벤트입니다. Hello 추적 보다 쉽게 필터링 하는 것에 대 한 hello 심각도 지정할 수 있습니다.

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
응용 프로그램 로깅 tooenable 너무 이동**모니터링** > **진단 로그** 응용 프로그램 로깅 사용 hello 설정/해제를 사용 하 고 있습니다.

![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

응용 프로그램 로그에는 tooblob 저장소 푸시할 또는 저장된 tooyour 웹 앱의 파일 시스템 수 있습니다. 프로덕션 시나리오 권장된 toouse blob 저장소입니다.

> [!IMPORTANT]
> 로깅을 사용하도록 설정하면 응용 프로그램 성능과 리소스 사용률에 영향을 미칠 수 있습니다. 프로덕션 시나리오에서는 오류 로그를 사용하는 것이 좋습니다. 자세한 로깅은 문제를 조사할 때만 사용하도록 설정합니다.

 ### <a name="web-server-diagnostics"></a>웹 서버 진단
앱이 계측되지 않는 경우에도 웹 서버 로그는 생성됩니다. App Service에서는 세 가지 종류의 서버 로그를 수집할 수 있습니다.

- **웹 서버 로깅**
    - Hello를 사용 하 여 HTTP 트랜잭션에 대 한 내용은 [W3C 확장된 로그 파일 형식](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx)합니다.
    - 특정 IP 주소에서 요청 처리 hello 수 또는 요청 수와 같은 전반적인 사이트 메트릭을 결정할 때 유용 합니다.
- **자세한 오류 로깅**
    - 오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)의 자세한 오류 정보입니다.
    - [자세한 오류 로깅에 대한 자세한 정보](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **실패한 요청 추적**
    - Tooprocess hello 요청 및 hello 소요 시간 각 구성 요소를 사용 하는 추적의 hello IIS 구성 요소를 포함 하 여 실패 한 요청을 대 한 자세한 정보.
    - 실패 한 요청 로그는 특정 HTTP 오류 원인을 tooisolate 하려고 할 때 유용 합니다.
    - [실패한 요청 추적에 대한 자세한 정보](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

tooenable 서버 로깅:
- 너무 이동**모니터링** > **진단 로그**합니다.
- Hello 다양 한 유형의 hello 설정/해제를 사용 하 여 웹 서버 진단을 사용 하도록 설정 합니다.

![앱 모니터링](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> 로깅을 사용하도록 설정하면 응용 프로그램 성능과 리소스 사용률에 영향을 미칠 수 있습니다. 프로덕션 시나리오에서는 오류 로그를 사용하는 것이 좋으며, 자세한 로깅은 문제를 조사할 때만 사용하도록 설정합니다.

### <a name="accessing-logs"></a>로그 액세스
Blob Storage에 저장된 로그에는 Azure Storage Explorer를 사용하여 액세스합니다. Hello 웹 앱의 파일 시스템에 저장 된 로그 경로 따라 hello에서 FTP를 통해 액세스 됩니다.

- **응용 프로그램 로그** - `%HOME%/LogFiles/Application/`.
    - 이 폴더에는 응용 프로그램 로깅으로 생성된 정보가 포함된 하나 이상의 텍스트 파일이 포함됩니다.
- **실패한 요청 추적** - `%HOME%/LogFiles/W3SVC#########/`.
    - 이 폴더에는 하나의 XSL 파일 및 하나 이상의 XML 파일이 포함되어 있습니다.
- **자세한 오류 로그** - `%HOME%/LogFiles/DetailedErrors/`.
    - 이 폴더에는 응용 프로그램에서 생성되는 HTTP와 관련된 정보가 광범위하게 포함된 .htm 파일이 하나 이상 있습니다.
- **웹 서버 로그** - `%HOME%/LogFiles/http/RawLogs`.
    - 이 폴더에는 hello W3C 확장된 로그 파일 형식을 사용 하 여 서식이 지정 된 텍스트 파일을 하나 이상 포함 되어 있습니다.

## <a name="streaming"></a>6 단계 - 스트리밍 로그
스트리밍 로그는 너무 비교 시간을 절약 하므로 응용 프로그램을 디버깅할 때 편리한[hello 로그에 액세스 하](#Accessing-Logs) FTP를 통해.

App Service에서는 **응용 프로그램 로그** 및 **웹 서버 로그**가 생성될 때 스트림할 수 있습니다.

> [!TIP]
> Toostream 로그를 시도 하기 전에 hello에 설명 된 대로 로그 수집 설정 되어 있는지 확인 [로깅](#logging) 섹션.

toostream 로그 이동 너무**모니터링**> **로그 스트림**합니다. 원하는 정보에 따라 **응용 프로그램 로그** 또는 **웹 서버 로그**를 선택합니다. 여기에서 일시 중지를 다시 시작 및 hello 버퍼를 지울 수 있습니다.

![스트리밍 로그](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> 로그는 hello 응용 프로그램에 트래픽을 있는 경우에 생성, 더 많은 이벤트 나 정보 로그 tooget의 hello 자세한 정도 늘릴 수도 있습니다.

## <a name="remote"></a>7 단계 - 원격 디버깅
사용 하 여 hello pin 기준 소스 hello 응용 프로그램 문제를 만든 후 **원격 디버깅** hello 코드를 통해 toowalk 합니다.

원격 디버깅을 사용 하면 연결할 디버거 tooyour 웹 응용 프로그램 hello 클라우드에서 실행 합니다. 중단점을 설정할 메모리를 직접 조작 및 코드를 단계적 로컬로 실행 되는 앱에 대해 수행 하는 것 처럼 hello 코드 경로 변경할 수도 있습니다.

tooattach hello 디버거 tooyour 앱 hello 클라우드에서 실행 중인:

- Visual Studio 2017 년 1 hello 앱에 대 한 솔루션 열기 hello 사용 하 여 원하는 toodebug
- 로컬 개발의 경우와 마찬가지로 중단점을 몇 개 설정합니다.
- **클라우드 탐색기**를 엽니다(ctr + /, ctrl + x).
- 필요하면 Azure 자격 증명으로 로그인합니다.
- 원하는 toodebug 찾기 hello 앱
- 선택 **디버거 연결** 양식 hello **동작** 창.

![원격 디버깅](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio 원격 디버깅을 위해 응용 프로그램을 구성 하 고 tooyour 응용 프로그램을 이동 하는 브라우저 창이 실행. 응용 프로그램 tootrigger 중단점 hello 코드를 단계별로 실행 합니다.

> [!WARNING]
> 프로덕션 사이트에서 디버그 모드로 실행하는 것은 권장되지 않습니다. 프로덕션 앱 toomultiple 서버 인스턴스에서 아웃 되지 배율 조정 하는 경우 응답 tooother 요청에서 웹 서버 hello 하지 못하도록 디버깅 합니다. 프로덕션 문제를 해결 하 여 가장 적합 한 리소스는 너무[로깅을 구성](#logging) 및 [Application Insights](#insights)합니다.



## <a name="explorer"></a> 8단계 - 프로세스 탐색기
응용 프로그램을 하나의 인스턴스가 아닌 toomore 확장할 때 **프로세스 탐색기** 인스턴스 문제를 식별 하는 데 도움이 됩니다.

**Process Explorer**를 사용하여 다음을 수행할 수 있습니다.

- 앱 서비스 계획의 다른 인스턴스에서 모든 hello 프로세스를 열거 합니다.
- 드릴 다운 하 고 hello 핸들 및 각 프로세스와 관련 된 모듈을 봅니다.
- 런어웨이 프로세스를 식별 하는 수준 toohelp를 처리 하는 hello 시 CPU 보기, 작업 집합 및 스레드 수
- 열려 있는 파일 핸들을 찾고, 필요하면 특정 프로세스 인스턴스를 종료합니다.

프로세스 탐색기는 **모니터링** > **프로세스 탐색기**에 있을 수 있습니다.

![Process Explorer](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a> 9단계 - Application Insights
**Application Insights**에서는 응용 프로그램에 대한 응용 프로그램 프로파일링 및 고급 모니터링 기능을 제공합니다.

예외 및 웹 앱의 성능 문제를 진단 및 toodetect Application Insights를 사용 합니다.

**모니터링** > **Application Insights**에서 웹앱에 대해 Application Insights를 사용하도록 설정할 수 있습니다.

> [!NOTE]
> Application Insights 데이터 수집 tooinstall hello Application Insights 사이트 확장 toostart를 라는 될 수 있습니다. 응용 프로그램을 다시 시작을 하면 hello 사이트 확장을 설치 합니다.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights에 다양 한 기능 집합, toolearn 더 링크를 따라 hello hello에 포함 된 [다음 단계](#next) 섹션.

## <a name="next"></a> 다음 단계

 - [Application Insights란?](..\application-insights\app-insights-overview.md)
 - [Application Insights를 사용한 Azure 웹앱 성능 모니터링](..\application-insights\app-insights-azure-web-apps.md)
 - [Application Insights를 사용한 웹 사이트의 가용성 및 응답성 모니터링](..\application-insights\app-insights-monitor-web-app-availability.md)
