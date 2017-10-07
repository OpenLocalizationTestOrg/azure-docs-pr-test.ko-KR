---
title: "앱 서비스에서 웹 응용 프로그램 성능 aaaSlow | Microsoft Docs"
description: "이 문서에서는 Azure App Service의 느린 웹앱 성능 문제를 해결하는 데 도움을 줍니다."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "웹앱 성능, 느린 앱, 앱 느림"
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>Azure App Service에서 느린 웹앱 성능 문제 해결
이 문서에서는 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)의 느린 웹앱 성능 문제를 해결하는 데 도움을 줍니다.

이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 을 클릭할 **Get Support**합니다.

## <a name="symptom"></a>증상
Hello 웹 응용 프로그램을 찾아볼 때 hello 페이지 부하 느린 및 경우에 따라 제한 시간입니다.

## <a name="cause"></a>원인
이 문제는 응용 프로그램 수준 문제가 원인이 되는 경우가 많습니다. 예를 들어:

* 긴 네트워크 요청 시간
* 비효율적인 응용 프로그램 코드 또는 데이터베이스 쿼리
* 높은 메모리/CPU를 사용하는 응용 프로그램
* tooan 예외 인해 충돌 하는 응용 프로그램

## <a name="troubleshooting-steps"></a>문제 해결 단계
문제 해결은 해결하는 순서대로 세 가지로 구분할 수 있습니다.

1. [응용 프로그램 작동을 관찰 및 감시](#observe)
2. [데이터 수집](#collect)
3. [Hello 문제를 완화](#mitigate)

[App Service Web Apps](/services/app-service/web/)는 각 단계별로 다양한 옵션을 제공합니다.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. 응용 프로그램 작동을 관찰 및 감시 
#### <a name="track-service-health"></a>서비스 상태를 추적합니다.
Microsoft Azure는 서비스가 중단되거나 성능이 저하될 때마다 경고를 표시합니다. Hello에서 hello 서비스의 hello 상태를 추적할 수 있습니다 [Azure 포털](https://portal.azure.com/)합니다. 자세한 내용은 [서비스 상태 추적](../monitoring-and-diagnostics/insights-service-health.md)을 참조하세요.

#### <a name="monitor-your-web-app"></a>웹앱 모니터링
응용 프로그램 문제가 있는 경우 아웃 toofind가 있습니다. 웹 앱 블레이드 클릭 hello **요청 및 오류** 바둑판식으로 배열입니다. hello **메트릭을** 블레이드를 보면 모든 hello 메트릭을 추가할 수 있습니다.

알았으므로 toomonitor 웹 앱에 대 한 hello 메트릭 중 일부는

* 평균 메모리 작업 집합
* 평균 응답 시간
* CPU 시간
* 메모리 작업 집합
* 요청

![웹앱 성능 모니터링](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

자세한 내용은 다음을 참조하세요.

* [Azure App Service에서 Web Apps 모니터링](web-sites-monitor.md)
* [경고 알림 받기](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>웹 끝점 상태 모니터링
Hello에 웹 앱을 실행 하는 경우 **표준** 가격 책정 계층을 웹 응용 프로그램을 모니터링할 수 3 개의 지리적 위치에서 두 개의 끝점입니다.

끝점 모니터링은 지리적으로 분산된 위치에서 웹 URL의 응답 시간 및 가동 시간을 테스트하는 웹 테스트를 구성합니다. hello 테스트는 각 위치에서 hello 웹 URL toodetermine hello 응답 시간과 작동 시간에 대 한 HTTP GET 작업을 수행합니다. 구성된 각 위치에서는 5분마다 테스트를 실행합니다.

가동 시간은 HTTP 응답 코드를 사용하여 모니터링되며 응답 시간은 밀리초로 측정됩니다. Hello HTTP 응답 코드는 보다 크거나 같은 too400 또는 hello 응답이 30 초 이상 걸릴 경우 모니터링 테스트가 실패 합니다. 끝점 모두에서 모니터링 테스트가 성공 하는 경우 사용할 수 있는 것으로 간주 됩니다 hello 위치를 지정 합니다.

그 참조 tooset [Azure 앱 서비스에서 앱 모니터링](web-sites-monitor.md)합니다.

또한, 끝점 모니터링의 비디오에 대해서는 [Azure Websites 가동 및 끝 점 모니터링 - 스테판 스차코우(Stefan Schackow)](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) 를 참조하세요.

#### <a name="application-performance-monitoring-using-extensions"></a>확장을 사용하여 응용 프로그램 성능 모니터링
응용 프로그램 성능을 *사이트 확장*을 사용하여 모니터링 할 수도 있습니다.

각 앱 서비스 웹 앱 사이트 확장으로 배포 하는 도구 집합이 강력한 toouse 수 있는 확장 가능한 관리 끝점을 제공 합니다. 확장은 다음을 포함합니다. 

- [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx)와 같은 소스 코드 편집기. 
- MySQL 데이터베이스와 같은 연결 된 리소스에 대 한 관리 도구 연결 tooa 웹 응용 프로그램.

[Azure Application Insights](/services/application-insights/) 및 [New Relic](/marketplace/partners/newrelic/newrelic/) 는 두 가지 hello 성능 사용할 수 있는 사이트 확장을 모니터링 합니다. New Relic toouse 런타임 시 에이전트를 설치 합니다. toouse Azure Application Insights SDK 사용 하 여 코드 다시 작성 하 고 tooadditional 데이터 액세스를 제공 하는 확장을 설치할 수 있습니다. hello SDK를 사용 하면 코드 toomonitor hello 사용 및 응용 프로그램의 성능을 보다 자세히를 작성할 수 있습니다.

Application Insights toouse 참조 [웹 응용 프로그램의 성능을 모니터링](../application-insights/app-insights-web-monitor-performance.md)합니다.

New Relic toouse 참조 [Azure에서 새로운 Relic 응용 프로그램 성능 관리](../store-new-relic-cloud-services-dotnet-application-performance-management.md)합니다.

<a name="collect" />

### <a name="2-collect-data"></a>2. 데이터 수집
웹 앱 환경을 hello hello 웹 서버와 hello 웹 응용 프로그램에서 로깅 정보에 대 한 진단 기능을 제공합니다. hello 정보는 웹 서버 진단 및 응용 프로그램 진단으로 분리 됩니다.

#### <a name="enable-web-server-diagnostics"></a>웹 서버 진단 사용
다음 종류의 로그 hello를 사용 하지 않도록 설정 하거나 설정할 수 있습니다.

* **자세한 오류 로깅** - 오류를 나타내는 HTTP 상태 코드(상태 코드 400 이상)의 자세한 오류 정보입니다. 이 hello 서버 hello 오류 코드를 반환 하는 이유를 확인 하는 데 유용한 정보를 포함할 수 있습니다.
* **요청을 추적 하지 못했습니다.** -hello IIS 구성 요소 사용 tooprocess hello 요청 및 각 구성 요소에서 수행 되는 hello 시간 추적을 포함 하 여 실패 한 요청을 대 한 상세 정보가 있습니다. 웹 응용 프로그램 성능 tooimprove 시도 중인 또는 특정 HTTP 오류 원인을 격리 하는 경우에 유용할 수 있습니다.
* **웹 서버 로깅** -hello W3C 확장된 로그 파일 형식을 사용 하 여 HTTP 트랜잭션에 대 한 정보입니다. 특정 IP 주소에서 요청 처리 hello 수 또는 요청 수 같은 전체 웹 앱 메트릭을 결정할 때 유용 합니다.

#### <a name="enable-application-diagnostics"></a>응용 프로그램 진단 사용
웹 앱에서 몇 가지 옵션 toocollect 응용 프로그램 성능 데이터, Visual Studio에서 라이브 응용 프로그램 프로 파일링 또는 자세한 정보를 추적 응용 프로그램 코드 toolog를 수정 하십시오. 따라 hello 옵션을 선택할 수 있습니다 toohello 응용 프로그램에 액세스 해야 하 고 hello 모니터링 도구에서에서 관찰 된 합니다.

##### <a name="use-application-insights-profiler"></a>Application Insights Profiler 사용
Hello 응용 프로그램 통찰력 프로파일러 toostart 자세한 성능 추적을 캡처할 수 있습니다. Hello 과거에 발생 한 일 전에 tooinvestigate 문제 중지 해야 toofive를 캡처된 추적을 액세스할 수 있습니다. Azure 포털에서 Application Insights 리소스 액세스 toohello 웹 응용 프로그램을 설정한 상태로이 옵션을 선택할 수 있습니다.

응용 프로그램 통찰력 프로파일러 발생 시킨 hello 응답 속도가 느려지고 코드 줄을 나타내는 각 웹 호출 및 추적에 대 한 응답 시간에 통계를 제공 합니다. 경우에 따라 hello 앱 서비스 앱 이므로 느린은 그리 특정 코드는 작성 되지 않고 방법입니다. 예를 들어 병렬로 실행될 수 있는 순차 코드와 원하지 않는 데이터베이스 잠금 경합이 있습니다. Hello 응용 프로그램의 성능이 향상 hello 코드에서 이러한 병목 현상을 제거 하지만 정교한 추적 및 로그를 설정 하지 않고 하드 toodetect 됩니다. hello 응용 프로그램 통찰력 프로파일러에 의해 수집 된 hello hello 응용 프로그램을 낮추고 된 코드 행을 식별 하는 데 도움이 됩니다 추적과 앱 서비스 앱에 대 한 이러한 문제를 해결 합니다.

 자세한 내용은 [Application Insights를 사용하여 라이브 Azure Web Apps 프로파일링](../application-insights/app-insights-profiler.md)을 참조하세요.

##### <a name="use-remote-profiling"></a>원격 프로파일링 사용하기
Azure App Service에서 Web Apps, API Apps 그리고 WebJob을 원격으로 프로파일할 수 있습니다. 어떻게 tooreproduce hello 문제를 알고 또는 정확한 hello를 알고 있는 경우이 시간 간격 hello 성능 문제가 발생 하 고 액세스 toohello 웹 응용 프로그램 리소스에 있는 경우이 옵션을 선택 합니다.

원격 프로 파일링 hello hello 프로세스의 CPU 사용률이 높습니다. 및 프로세스에는 예상 보다 느리게 실행 되는, HTTP 요청의 hello 대기 시간이 보통 때 보다 더 높은 원격으로 프로세스를 프로 파일링 하 고 받을 수 hello CPU 샘플링 호출 스택 tooanalyze 유용 프로세스 활동 hello 및 코드 실행 부하 과다 경로입니다.

자세한 내용은 [Azure App Service에서 원격 프로파일링 지원](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service)을 참조하세요.

##### <a name="set-up-diagnostic-traces-manually"></a>진단 추적을 수동으로 설정
액세스 toohello 웹 응용 프로그램 소스 코드를 있는 경우 응용 프로그램 진단 사용 하면 toocapture 정보는 웹 응용 프로그램에서 생성 합니다. ASP.NET 응용 프로그램에서는 hello `System.Diagnostics.Trace` 클래스 toolog 정보 toohello 응용 프로그램 진단 로그입니다. 그러나 toochange 해야 코드 hello 및 응용 프로그램을 다시 배포 합니다. 테스트 환경에서 앱을 실행 중인 경우 이 메서드를 권장합니다.

방법에 대 한 자세한 지침은 tooconfigure 로깅에 대 한 응용 프로그램 참조 [Azure 앱 서비스의 웹 앱에 대 한 진단 로깅 사용](web-sites-enable-diagnostic-log.md)합니다.

#### <a name="use-hello-azure-app-service-support-portal"></a>Hello Azure 앱 서비스 지원 포털을 사용 하 여
웹 앱을 사용 하면 HTTP 로그, 이벤트 로그, 프로세스 덤프 및 자세히 확인 하 여 hello 기능 tootroubleshoot 문제 관련된 tooyour 웹 앱으로 할 수 있습니다. **http://&lt;your app name>.scm.azurewebsites.net/Support**에서 지원 포털을 사용하여 모든 정보에 액세스할 수 있습니다.

hello Azure 앱 서비스 지원 포털 toosupport hello 일반적인 문제 해결 시나리오의 세 가지 단계가 세 개의 별도 탭 나와 있습니다.

1. 현재 동작을 관찰하기
2. 진단 정보 수집 및 기본 제공 분석기 hello를 실행 하 여 분석
3. 완화

지금 바로 hello 문제 상황을 클릭 하 여 **분석** > **진단** > **이제 진단** toocreate, 진단 세션을 HTTP 로그, 이벤트 뷰어 로그, 메모리 덤프, PHP 오류 로그 및 PHP 프로세스 보고서를 수집 합니다.

Hello 데이터 수집 되 면 hello 지원 포털 hello 데이터에 대해 분석을 실행 하 고 HTML 보고서를 제공 합니다.

기본적으로 toodownload hello 데이터를 원하는 경우에 hello D:\home\data\DaaS 폴더에 저장 됩니다.

Azure 앱 서비스 지원 포털 hello에 대 한 자세한 내용은 참조 하십시오. [새 업데이트 tooSupport Azure 웹 사이트에 대 한 사이트 확장](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites)합니다.

#### <a name="use-hello-kudu-debug-console"></a>Hello Kudu 디버그 콘솔을 사용 하 여
Web Apps는 사용자 환경에 대한 정보를 얻을 수 있는 JSON 끝점과 비슷한 디버깅, 탐색, 파일 업로드할 수 있는 디버그 콘솔과 함께 제공됩니다. 이 콘솔 hello 라고 *Kudu 콘솔* 또는 hello *SCM 대시보드* 웹 앱에 대 한 합니다.

Toohello 링크 이동 하 여이 대시보드에 액세스할 수 **https://&lt;응용 프로그램 이름 >.scm.azurewebsites.net/**합니다.

Kudu는 제공 하는 hello 것은 다음과 같습니다.

* 응용 프로그램에 대한 환경 설정
* 로그 스트림
* 진단 덤프
* Powershell cmdlet 및 기본 DOS 명령을 실행할 수 있는 콘솔을 디버깅합니다.

Kudu의 또 다른 유용한 특징은, 응용 프로그램 첫째 예외를 throw 하는 경우에 대비 Kudu를 사용할 수 있습니다 hello SysInternals 도구 Procdump toocreate 메모리 덤프입니다. 이러한 메모리 덤프 hello 프로세스의 스냅숏입니다 및 웹 앱과 함께 보다 복잡 한 문제를 해결 하는 데 도움이 될 수 있습니다.

Kudu에서 사용 가능한 기능에 대한 자세한 내용은 [사용자가 꼭 알아야 할 Azure Websites 팀 서비스 도구](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/)를 참조하세요.

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Hello 문제를 완화
#### <a name="scale-hello-web-app"></a>배율 hello 웹 응용 프로그램
향상 된 성능 / 처리량에 대 한 Azure 앱 서비스의 응용 프로그램을 실행 하는 hello 눈금을 조정할 수 있습니다. 두 개의 관련 된 동작에서는 웹 앱 확장: toohello 높은 가격 책정 계층을 전환한 후 특정 설정을 구성 하 고 가격 책정 계층을 더 높은 완료 된 앱 서비스 계획 tooa 변경 합니다.

크기 조정에 대한 자세한 내용은 [Azure App Service에서 웹앱 크기 조정](web-sites-scale.md)을 참조하세요.

또한 둘 이상의 인스턴스에서 응용 프로그램 toorun를 선택할 수 있습니다. 크기 확장은 더 많은 처리 기능을 제공할 뿐만 아니라, 어느 정도의 내결함성을 제공합니다. Hello 프로세스의 한 인스턴스에 작동이 hello 다른 인스턴스는 계속 tooserve 요청 합니다.

Hello toobe 수동 또는 자동 크기 조정을 설정할 수 있습니다.

#### <a name="use-autoheal"></a>AutoHeal를 사용
AutoHeal (예: 구성 변경, 요청, 메모리 기반 제한 또는 hello 시간 tooexecute 요청 필요)를 선택 하는 설정에 따라 응용 프로그램에 대 한 hello 작업자 프로세스를 재활용 합니다. 대부분의 hello 재활용 hello 프로세스는 문제로 인해 hello 가장 빠른 방법은 toorecover 합니다. 경우에 항상 hello Azure 포털 내에서 직접 hello 웹 앱에서 다시 시작할 수 있습니다, AutoHeal는 자동으로 드립니다. 웹 앱에 대 한 hello 루트 web.config에 몇 가지는 트리거를 추가 하면 toodo 됩니다. 이러한 설정은 작동 하는 hello 동일한 방식으로 응용 프로그램이 없는 경우.Net 응용 프로그램입니다.

자세한 내용은 [Auto-Healing Azure Websites](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/)를 참조하세요.

#### <a name="restart-hello-web-app"></a>Hello 웹 앱을 다시 시작
다시 시작은 일회성 문제에서 가장 간단한 방법은 toorecover hello 경우가 많습니다. Hello에 [Azure 포털](https://portal.azure.com/), 웹 앱의 블레이드에서 hello 옵션 toostop 했거나 응용 프로그램을 다시 시작 합니다.

 ![웹 앱 toosolve 성능 문제를 다시 시작](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

또한, Azure Powershell을 사용하여 웹앱을 관리할 수 있습니다. 자세한 내용은 [Azure 리소스 관리자에서 Azure PowerShell 사용](../powershell-azure-resource-manager.md)을 참조하세요.
