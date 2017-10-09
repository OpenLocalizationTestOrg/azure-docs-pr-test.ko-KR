---
title: "Application Insights를 사용 하 여 Azure에서 aaaProfiling 라이브 웹 앱 | Microsoft Docs"
description: "사용량이 프로파일러를 웹 서버 코드에서 hello 실행 부하 과다 경로 식별 합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Application Insights를 사용하여 라이브 Azure Web Apps 프로파일링

*Application Insights의 이 기능은 App Services의 경우 GA이고 Compute의 경우 미리 보기에 있습니다.*

프로 파일링 도구의의 hello를 사용 하 여 라이브 웹 응용 프로그램에서 각 방법의 소요 시간 확인 [Azure Application Insights](app-insights-overview.md)합니다. 응용 프로그램에서 제공 된 라이브 요청의 자세한 프로필 표시 하 고 hello를 사용 하는 hello 대부분의 시간 ' 실행 부하 과다 경로'를 강조 표시 합니다. 서로 다른 응답 시간을 갖는 예제를 자동으로 선택합니다. hello 프로파일러는 다양 한 기술을 toominimize 오버 헤드를 사용합니다.

hello 프로파일러 현재 ASP.NET에 대 한 works 웹 Azure 앱 서비스에서 실행 되는 앱에서 Basic 가격 책정 계층 이상 hello 합니다. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Hello 프로파일러를 사용 하도록 설정

코드에서 [Application Insights를 설치합니다](app-insights-asp-net.md). 이미 설치 되어 있으면 hello 최신 버전이 있는지 확인 합니다. (toodo이를 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 NuGet 패키지 관리를 선택 합니다. 업데이트를 선택하고 모든 패키지를 업데이트합니다.) 앱을 다시 배포합니다.

*ASP.NET Core를 사용 중입니까? [여기를 확인하세요](#aspnetcore).*

[https://portal.azure.com](https://portal.azure.com), 웹 앱에 대 한 hello Application Insights 리소스를 엽니다. **성능**을 열고 **Application Insights 프로파일러 사용...**을 클릭합니다.

![Hello 사용 프로파일러 배너에 클릭][enable-profiler-banner]

항상 클릭 해도, **구성** tooview 상태를 사용 하도록 설정 또는 hello 프로파일러를 사용 하지 않도록 설정 합니다.

![Hello 성능 블레이드에서 구성을 클릭합니다][performance-blade]

Application Insights로 구성된 웹앱은 구성 블레이드에 나열됩니다. 필요한 경우 지침 tooinstall hello 프로파일러 에이전트를 따릅니다. Application Insights로 구성된 웹앱이 아직 없는 경우 *연결된 앱 추가*를 클릭합니다.

사용 하 여 hello *프로파일러를 사용 하도록 설정* 또는 *프로파일러 사용 하지 않도록 설정* hello 구성 블레이드 toocontrol 단추 모든 연결 된 웹 앱에 프로파일러를 hello 합니다.



![구성 블레이드][linked app services]

개별 응용 프로그램 서비스 인스턴스에 대 한 hello 프로파일러 toostop 또는 다시 시작에서 찾을 수 **hello 응용 프로그램 서비스 리소스에에서**에 **웹 작업이**합니다. toodelete 것 검토 **확장**합니다.

![웹 작업에 대한 프로파일러 사용 안 함][disable-profiler-webjob]

Hello 프로파일러 성능 문제를 가능한 한 빨리 프로그램 모든 웹 앱 toodiscover에서 사용 하도록 설정 해야 하는 것이 좋습니다.

WebDeploy toodeploy 변경 tooyour 웹 응용 프로그램을 사용 하는 경우 확인 hello를 제외 하면 **App_Data** 폴더를 배포 하는 동안 삭제 되지 않도록 합니다. 그렇지 않으면 hello 프로파일러 확장의 파일이 삭제 됩니다 hello 웹 응용 프로그램 tooAzure를 다음에 배포 하는 경우.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Azure VM 및 Compute 리소스에서 프로파일러 사용(미리 보기)

[런타임에 Azure App Services에 대해 Application Insights를 사용하도록 설정](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights)하면 프로파일러를 자동으로 사용할 수 있습니다. (Hello 리소스에 대 한 Application Insights 이미 설정한 경우에 hello 통해 tooupdate toohello lates 버전을 할 수 있습니다 **구성** 마법사.)

한 [미리 보기 버전의 Azure 계산 리소스에 대 한 프로파일러 hello](https://go.microsoft.com/fwlink/?linkid=848155)합니다.


## <a name="limits"></a>제한

hello 기본 데이터 보존은 5 일입니다. 매일 최대 10GB가 수집됩니다.

hello 프로파일러 서비스에 대 한 무료입니다. 웹 앱에서 호스트 되어야 합니다 적어도 응용 프로그램 서비스의 기본 계층 hello 합니다.

## <a name="viewing-profiler-data"></a>프로파일러 데이터 보기

Toohello 작업 목록 아래로 스크롤하여 및 hello 성능 블레이드를 엽니다.




![Application Insights 성능 블레이드 예제 열][performance-blade-examples]

hello hello 테이블의 열이 됩니다.

* **Count** -hello hello 블레이드의 hello 시간 범위에서 이러한 요청 수입니다.
* **중앙값** -hello 일반적인 시간이 앱 toorespond tooa 요청 합니다. 모든 응답의 절반은 이것보다 더 빨랐습니다.
* **95 백분위수** 응답의 95%는 이것보다 더 빨랐습니다. 이 그림 hello 중앙값 매우 다른 경우 응용 프로그램에 일시적인 문제가 있을 수 있습니다. (또는 캐시와 같은 디자인 기능으로 설명될 수 있습니다.)
* **예제** -아이콘 hello 프로파일러가이 작업에 대 한 스택 추적 캡처를 나타냅니다.

Hello 예제 아이콘 tooopen hello 추적 탐색기를 클릭 합니다. 프로파일러 hello 몇 가지 예제를 캡처한 hello 탐색기 표시 응답 시간에 따라 분류 합니다.

샘플 tooshow 코드 수준 분석을 실행 중인 데 걸린된 hello 요청이 시간을 선택 합니다.

![Application Insights 추적 탐색기][trace-explorer]

**실행 부하 과다 경로 표시** 열립니다 리프 노드로 서 가장 큰, hello 또는 적어도 무언가 닫습니다. 대부분의 경우에서이 노드의 인접 tooa 성능 병목 상태가 됩니다.



* **레이블**: hello 함수 또는 이벤트의 hello 이름입니다. hello 트리 코드 및 (예: SQL 및 http 이벤트)에 발생 한 이벤트의 혼합을 표시 합니다. hello 최상위 이벤트 나타내는 hello 전체 기간을 요청 합니다.
* **경과 된**: hello 연산의 hello 시작과 hello 끝 사이의 hello 시간 간격입니다.
* **때**: hello 함수/이벤트 관계 tooother 함수에서 실행 되는 경우를 보여 줍니다.

## <a name="how-tooread-performance-data"></a>어떻게 tooread 성능 데이터

Microsoft 서비스 프로파일러에서 응용 프로그램의 메서드 및 계측 tooanalyze hello 성능을 샘플링의 조합을 사용 합니다.
자세한 컬렉션 진행에서 되 면 서비스 프로파일러 샘플 hello 모든 밀리초 동안의 hello 컴퓨터의 CPU의 각 명령 포인터입니다.
각 샘플의 현재 실행, 스레드를 수행 하는지 모두에서 고가 저가의 수준의 추상화에 대 한 상세 하 고 유용한 정보를 제공 하는 hello 스레드 hello 완전 한 호출 스택을 캡처합니다. 서비스 프로파일러에서 또한 다른 컨텍스트 스위칭 이벤트 등의 이벤트, TPL 이벤트 및 스레드 풀 이벤트 tootrack 활동 상관 관계 및 인과 관계를 수집합니다.

hello 타임 라인 보기에 표시 된 hello 호출 스택은 샘플링 및 계측 위에 hello hello 결과입니다. 각 샘플 hello 스레드의 전체 호출 스택을 hello를 캡처하므로, 참조할 다른 프레임 워크와 hello.NET framework에서 코드가 포함 되어 있습니다.

### <a id="jitnewobj"></a>개체 할당(`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1`은 관리되는 힙에서 메모리를 할당하는 .NET 프레임워크 내부의 도우미 함수입니다. 개체가 할당되면 `clr!JIT\_New`가 호출됩니다. 개체 배열이 할당되면 `clr!JIT\_Newarr1`이 호출됩니다. 이 두 함수는 일반적으로 매우 빠르며 상대적으로 적은 양의 시간을 사용해야 합니다. 표시 되 면 `clr!JIT\_New` 또는 `clr!JIT\_Newarr1` 일정에서 상당한 양의 시간, 표시 hello 코드 많은 개체를 할당 및 메모리가 많이 소비 될 수 있습니다.

### <a id="theprestub"></a>코드 로드(`clr!ThePreStub`)
`clr!ThePreStub`처음으로 hello에 대 한 hello 코드 tooexecute를 준비 하는.NET framework 내 도우미 함수가입니다. 일반적으로 JIT(Just In Time) 컴파일을 포함하지만 이에 제한되지 않습니다. 각 C# 메서드에 대해 `clr!ThePreStub` hello 프로세스 수명 중에 많아야 한 번 호출 해야 합니다.

표시 되 면 `clr!ThePreStub` 상당한 걸립니다 요청에 대 한 시간의 해당 메서드 및.NET framework 런타임 tooload 메서드는 중요에 대 한 hello 시간을 실행 하는 첫 번째 hello 해당 요청을 나타냅니다. 사용자가 액세스할 하거나 NGen 어셈블리에서 실행 하기 전에 hello 코드의 해당 부분을 실행 하는 준비 프로세스를 고려할 수 있습니다.

### <a id="lockcontention"></a>잠금 경합(`clr!JITutil\_MonContention` 또는 `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`또는 `clr!JITutil\_MonEnterWorker` hello 현재 스레드가 해제 잠금 toobe에 대 한 대기를 나타냅니다. 이는 일반적으로 C# lock 문을 실행하거나 Monitor.Enter 메서드를 호출하거나 MethodImplOptions.Synchronized 특성으로 메서드를 호출할 때 표시됩니다. 잠금 경합 스레드 A 획득 한 잠금을 했는데 스레드 B가 A 스레드를 해제 하기 전에 잠금 동일 tooacquire hello에 일반적으로 발생 합니다.

### <a id="ngencold"></a>코드 로드(`[COLD]`)
Hello 메서드 이름에 포함 되어 있으면 `[COLD]`와 같은 `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`,으로 최적화 되지 않은 코드를 실행 하는 hello.NET framework 런타임 의미 <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">프로필 기반 최적화</a> 처음으로 hello에 대 한 합니다. 각 방법에 대 한 hello 프로세스의 hello 수명 동안 한 번 이하로 표시 됩니다.

코드를 로드 합니다. 변수를 사용할 경우 상당한 시간이 요청에 대 한 해당 요청은 hello 첫 번째 하나의 tooexecute hello 최적화 되지 않은 부분 hello 메서드를 나타냅니다. 사용자에 게 액세스 하기 전에 hello 코드의 해당 부분을 실행 하는 프로세스를 웜을 고려할 수 있습니다.

### <a id="httpclientsend"></a>HTTP 요청 보내기
와 같은 메서드 `HttpClient.Send` hello 코드가 HTTP 요청 toocomplete에 대 한 대기를 나타냅니다.

### <a id="sqlcommand"></a>데이터베이스 작업
SqlCommand.Execute 같이 hello 코드가 데이터베이스 작업 toocomplete에 대 한 대기를 나타냅니다.

### <a id="await"></a>대기(`AWAIT\_TIME`)
`AWAIT\_TIME`hello 코드가 다른 작업 toocomplete에 대 한 대기를 나타냅니다. 이는 일반적으로 C# 'await' 문과 함께 발생합니다. Hello 코드가 수행 하는 경우 C# 'await', hello 스레드 해제 및 제어 toohello 스레드 풀, 반환 및 hello 'await' toofinish 기다리는 차단 된 스레드가 없는 합니다. 그러나 스레드는 않은 hello await '' 대기 중인 차단 작업 toocomplete hello에 대 한 논리적으로 hello 합니다. `AWAIT\_TIME` hello 작업 toocomplete 기다리는 hello 차단 시간을 나타냅니다.

### <a id="block"></a>차단된 시간
`BLOCKED_TIME`hello 코드가 대기 하는 동기화 개체에 대 한, 사용 가능한 또는 요청 toofinish에 대 한 대기 중인 스레드 toobe 기다리는 같이 사용 가능한 다른 리소스 toobe에 대 한 대기를 나타냅니다.

### <a id="cpu"></a>CPU 시간
hello CPU는 hello 명령을 실행 합니다.

### <a id="disk"></a>디스크 시간
hello 응용 프로그램은 디스크 작업을 수행 합니다.

### <a id="network"></a>네트워크 시간
hello 응용 프로그램에 네트워크 작업 수행 됩니다.

### <a id="when"></a>때 열
이 노드에 대 한 수집 hello 포괄 샘플 시간의 경과 따라 어떻게의 시각화는. hello 요청의 전체 범위 hello 32 시간 버킷으로 나뉘고 hello 포괄 샘플 해당 노드에 대 한 이러한 32 버킷으로 누적 됩니다. 각 버킷은 높이가 크기 조정된 값을 나타내는 막대로 나타납니다. 표시 된 노드에 대 한 `CPU_TIME` 또는 `BLOCKED_TIME`, 또는 리소스 (cpu, 디스크, 스레드)를 사용 하는 관계는 확실 한 경우 해당 버킷의 hello 기간 동안 이러한 리소스 중 하나를 사용해 나타내는 막대 환영 합니다. 이러한 메트릭의 경우 여러 리소스를 소비하여 100% 이상을 얻을 수 있습니다. 예를 들어 두 개의 CPU를 사용하는 평균이 간격을 넘는 경우 200%를 얻습니다.


## <a id="troubleshooting"></a>문제 해결

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Application Insights Profiler가 실행되고 있는지 어떻게 알 수 있습니까?

hello 프로파일러 웹 앱에서 연속 웹 작업으로 실행 됩니다. Https://portal.azure.com의 hello 웹 응용 프로그램 리소스를 열고 hello WebJobs 블레이드에서 "ApplicationInsightsProfiler" 상태를 확인할 수 있습니다. 이 실행 중이 아닌 경우 열 **로그** 자세히 toofind 합니다.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>Hello 프로파일러를 실행 하는 경우에 모든 스택 예제를 찾을 수 없는 이유

다음 몇 가지 사항으로 확인할 수 있습니다.

1. 웹앱 서비스 계획이 기본 계층 이상인지 확인합니다.
2. 웹앱에서 Application Insights SDK 2.2 베타 이상이 활성화되었는지 확인합니다.
3. 웹 앱에 Application Insights SDK에서 동일한 계측 키를 사용 하는 hello로 hello APPINSIGHTS_INSTRUMENTATIONKEY 설정이 있는지 확인 합니다.
4. 웹앱이 .NET Framework 4.6에서 실행 중인지 확인합니다.
5. ASP.NET Core 응용 프로그램 이면도 확인 하십시오 [hello 필요한 종속성](#aspnetcore)합니다.

Hello 프로파일러 시작 된 후에 다음과 같은 hello 프로파일러 몇 가지 성능 추적 적극적으로 수집 되는 경우 특정 짧은 준비 기간. 그 후 hello 프로파일러에 1 시간 마다 2 분 동안 성능 추적을 수집합니다.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>Azure Service Profiler를 사용하고 있었습니다. 발생 했습니다 tooit 무엇입니까?  

Application Insights Profiler를 활성화하면 Azure Service Profiler 에이전트는 비활성화됩니다.

### <a id="double-counting"></a>병렬 스레드에서 이중 계산

일부의 경우 hello hello 스택 뷰어에서 총 시간 메트릭은 hello 실제 hello 요청 기간 보다 더 합니다.

병렬로 작업하는 두 개 이상의 스레드가 요청과 연결된 경우 발생할 수 있습니다. hello 총 스레드 시간은 다음 hello 경과 된 시간 보다 나중입니다. 대부분의 경우에 하나의 스레드를 기다리고 있을 수 있습니다 다른 toocomplete를 hello 합니다. 이 뷰어 시도 toodetect hello 및 hello 필요 하지 않은 대기를 생략 하지만 너무 많은 중요 한 정보가 있을 수 있습니다 어떻게 생략 하는 대신 보여 주는의 hello 측에 않는다는 문제가 있습니다.  

병렬 스레드 수를 추적에 표시 되 면 hello hello 요청에 대 한 중요 한 경로 확인할 수 있도록 스레드 대기 하 고 있는 toodetermine를 해야 합니다. 대부분의 경우에서는에서 단순히 대기 하는 대기 상태에 신속 하 게 hello 스레드가 다른 스레드에서 hello 합니다. 집중 다른 hello 되 고 대기 중인 스레드에 hello에 hello 시간을 무시 합니다.

### <a id="issue-loading-trace-in-viewer"></a>프로파일링 데이터 없음

1. Tooview 몇 주 보다 오래 된 hello 데이터 시도 하 고, 제한 시간 필터 고 다시 시도 하십시오.

2. 프록시 또는 방화벽 액세스 toohttps://gateway.azureserviceprofiler.net 차단 되지 않았는지 확인 합니다.

3. Application Insights 계측 키 응용 프로그램에서 사용 하는 hello와 프로 파일링을 활성화 한 Application Insights 리소스와 동일한 hello 해당 hello를 확인 합니다. hello 키 일반적으로 ApplicationInsights.config 이지만 web.config 또는 app.config에서 찾을 수도 있습니다.

### <a name="error-report-in-hello-profiling-viewer"></a>뷰어를 프로 파일링 하는 hello에서 오류 보고서

Hello 포털에서 지원 티켓을 파일입니다. Hello 오류 메시지에서 hello 상관 관계 ID를 포함 하십시오.

## <a name="manual-installation"></a>수동 설치

Hello 프로파일러를 구성 하는 경우 hello 다음 업데이트가 이루어지는 toohello 웹 앱 설정 합니다. 환경에 필요한 경우, 예를 들어 응용 프로그램이 ASE(Azure App Service Environment)에서 실행되는 경우 이 작업을 수동으로 직접 수행할 수 있습니다.

1. 웹 응용 프로그램 제어 블레이드에서 hello 설정을 엽니다.
2. 설정 ".NET Framework 버전" toov4.6 합니다.
3. "Always On" tooOn를 설정 합니다.
4. 응용 프로그램 설정을 추가 "__APPINSIGHTS_INSTRUMENTATIONKEY__" 및 집합 hello 값 toohello hello SDK에서 사용 하는 동일한 계측 키입니다.
5. 고급 도구를 엽니다.
6. Tooopen hello Kudu 웹 사이트 "Go"를 클릭 합니다.
7. Hello Kudu 웹 사이트에서 "사이트 확장"을 선택 합니다.
8. 갤러리에서 “__Application Insights__”를 설치합니다.
9. Hello 웹 응용 프로그램을 다시 시작 합니다.

## <a id="aspnetcore"></a>ASP.NET Core 지원

ASP.NET Core 응용 tooinstall Microsoft.ApplicationInsights.AspNetCore Nuget 패키지 2.1.0-beta6 또는 더 높은 toowork hello 프로파일러로 필요합니다. 더 이상 후 2017/6/27 hello 더 낮은 버전을 지원합니다.

## <a name="next-steps"></a>다음 단계

* [Visual Studio에서 Application Insights로 작업](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
