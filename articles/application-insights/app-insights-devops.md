---
title: "aaaWeb 응용 프로그램 성능 모니터링-Azure Application Insights | Microsoft Docs"
description: "Application Insights hello devOps 주기에 적용 되는 방식"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 479522a9-ff5c-471e-a405-b8fa221aedb3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: bba2d6c59de1794adcbf8e298d0ef4f0dbaa700f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deep-diagnostics-for-web-apps-and-services-with-application-insights"></a>Application Insights로 웹앱 및 서비스 심층 진단
## <a name="why-do-i-need-application-insights"></a>Application Insights가 필요한 이유는 무엇일까요?
Application Insights는 실행 중인 웹앱을 모니터링합니다. 오류와 성능 문제에 대해 알려주고 고객이 앱을 어떻게 사용하는지 분석하도록 도와줍니다. 많은 플랫폼 (J2EE, ASP.NET, Node.js,...)에서 실행 되는 앱에 대해 작동 하 고 hello 클라우드 또는 온-프레미스에 호스트 됩니다. 

![웹 응용 프로그램을 제공 하는 hello 복잡성 측면](./media/app-insights-devops/010.png)

필수 toomonitor 최신 응용 프로그램이 실행 되는 동안 가장 중요 한 점은 toodetect 실패 전에 원하는 대부분의 고객에 게 합니다. 또한 toodiscover 원하는 하 고 있는 동안 하지 치명적인 아마도 저하 또는 일부 불편 하면 tooyour 사용자 성능 문제를 해결 합니다. 원하는 tooknow hello 사용자가을 수행 하는 hello 시스템 tooyour 만족도 수행 하는 경우 및: hello 최신 기능을 사용 하 여 관리 됩니까? 잘 사용하고 있는지 궁금할 것입니다.

최신 웹 응용 프로그램은 지속적인 업데이트 주기의 개발: 새로운 기능 또는 향상; 해제 hello 사용자를 위한 얼마나 잘 작동을 관찰 합니다. 이 정보에 따라 개발의 hello 다음 증분을 계획 합니다. 이 주기의 핵심 부분에는 hello 관찰 단계입니다. Application Insights hello 도구 toomonitor 성능 및 사용에 대 한 웹 응용 프로그램을 제공 합니다.

이 프로세스의 hello 가장 중요 한 측면에는 진단 및 진단입니다. Hello 응용 프로그램이 실패 하는 경우 비즈니스 손실 되 고 됩니다. 모니터링 프레임 워크의 hello 프라임 역할 따라서 toodetect 실패는 안정적으로, hello 정보로 필요한 toodiagnose hello 문제를 즉시 여러분과 toopresent 알림. 바로 Application Insights가 이런 작업을 수행합니다.

### <a name="where-do-bugs-come-from"></a>버그는 어디에서 발생할까요?
일반적으로, 웹 시스템 오류는 구성 문제나 여러 구성 요소 간의 잘못된 상호 작용에서 발생합니다. 라이브 사이트 문제를 개발할 때 첫 번째 작업 hello hello 문제의 tooidentify hello 궤적 되므로: 어떤 구성 요소 또는 관계 원인인 hello?

지금 지긋이 나이를 먹은 분들은 컴퓨터 한 대에 하나의 프로그램만 실행하던 단순한 시절을 기억하실 겁니다. hello 개발자는 철저 하 게 테스트; 출시 하기 전에 및 자주 참조 또는 다시 생각해를 것, 배송 필요 합니다. hello 사용자는는 tooput 최대 hello 잔여 버그 수 년 동안. 

오늘날 상황은 매우 다릅니다. 응용 프로그램에 다양 한 장치 toorun 다양 한에 않으며 어려운 tooguarantee hello 정확히 동일한 동작 각 수 있습니다. Hello 클라우드에서 응용 프로그램 호스팅 버그를 신속 하 고 해결할 수 있지만 연속 경쟁과 hello 기대 하는 새로운 기능 잦은 간격,이 의미 합니다. 

이러한 조건에서 hello 방법은 tookeep만 hello 버그 수의 절대적인 컨트롤은 자동화 된 단위 테스트 합니다. 가능한 것 toomanually 다시 배달 마다에 있는 모든 항목 테스트 합니다. 단위 테스트의 hello 연산이 일부 빌드 프로세스 이제는 합니다. 여러 브라우저 버전에 대 한 테스트는 자동화 된 UI를 제공 하 여 hello Xamarin 테스트 클라우드 등의 도구 도움말입니다. 이러한 테스트 체계가 있습니다 수 있도록 허용 toohope 해당 hello 속도 응용 프로그램 내에서 발견 된 버그의 상태로 유지할 수 있지만 tooa 최소 합니다.

일반적인 웹 응용 프로그램에는 여러 라이브 구성 요소가 있습니다. 또한 toohello 클라이언트 (응용 프로그램) 장치 또는 브라우저와 hello 웹 서버에는 가능성이 toobe 상당한 백 엔드 처리. 가장 hello 백 엔드 구성 요소는 파이프라인 또는 공동 조각의 낮출 컬렉션입니다. 그 대부분은 개발자가 통제하지 못하고, 의존해야 하는 외부 서비스일 것입니다.

이와 같은 구성에서는,에 대 한 많은 시간과 uneconomical tootest 수 또는 예측 가능한 실패 모드 모든, 이외의 hello 시스템 자체를 라이브 수 것입니다. 

### <a name="questions-"></a>질문...
웹 시스템을 개발할 때 묻는 질문:

* 내 앱이 충돌하는가? 
* 정확히 무슨 일이 일어났는가? -요청, 실패 한 경우 있습니다 도달한 방법을 tooknow를 하겠습니다. 이벤트 추적이 필요합니다.
* 내 앱의 속도는 충분히 빠른가? Toorespond tootypical 요청 시간이 얼마나 오래 걸리나요?
* Hello 서버 핸들 hello 로드할 수 있습니까? 요청의 hello 속도 늘어남지 않습니다 hello 응답 시간을 보유 시에도 계속?
* 반응성는 내 종속성-hello REST Api, 데이터베이스 및이 응용 프로그램을 호출 하는 다른 구성 요소입니다. 특히, hello 시스템 느린 경우는 내 구성 요소 또는 다른 사람 으로부터 응답 속도가 느려지고는 동안?
* 앱이 확장 또는 축소가 가능한가? 것에서 볼 수 hello 전 세계? 앱이 중단될 경우 원인을 알아야 합니다.
* Hello 근본 원인이 무엇입니까? 내 구성 요소 또는 종속성 오류 hello 이었습니까? 통신 문제인가?
* 얼마나 많은 사용자가 영향을 받았는가? 있으면 둘 이상의 문제 tootackle 하는 가장 중요 한 hello?

## <a name="what-is-application-insights"></a>Application Insights란?
![Application Insights의 기본 워크플로](./media/app-insights-devops/020.png)

1. Application Insights는 응용 프로그램을 계측 하 고 hello 응용 프로그램을 실행 하는 동안 항목에 대 한 원격 분석을 보냅니다. Hello 앱에 Application Insights SDK hello를 구현할 수 있습니다 또는 런타임으로 계측을 적용할 수 있습니다. 사용자 고유의 원격 분석 toohello 일반 모듈을 추가할 수 있습니다 hello 이전 메서드는 보다 유연 합니다.
2. hello 원격 분석 toohello Application Insights 포털, 저장 및 처리에 전송 됩니다. (Application Insights는 Microsoft Azure에서 호스팅되지만 Azure 앱뿐만 아니라 모든 웹앱을 모니터링할 수 있습니다.)
3. hello 원격 분석 tooyou 차트 hello 양식 및 이벤트의 테이블에 표시 됩니다.

원격 분석에는 두 가지 주요 유형(집계 및 원시 인스턴스)이 있습니다. 

* 예를 들어, 인스턴스 데이터에는 웹앱이 수신한 요청 보고서가 포함됩니다. 에 대 한 찾아 수 hello 검색 도구를 사용 하 여 hello Application Insights 포털에서 요청 hello 세부 정보를 검사 합니다. hello 인스턴스는 앱의 toorespond toohello 요청 걸린 기간 같은 데이터가 포함으로 hello 요청된 URL, hello 클라이언트의 대략적인 위치 및 기타 데이터.
* 집계 된 데이터 hello hello 응답 시간이 요청 속도 비교할 수 있도록 시간 단위 당 이벤트 수를 포함 합니다. 요청 응답 시간 등의 메트릭 평균도 포함됩니다.

데이터의 hello 주요 범주는 있습니다.

* 요청 tooyour 응용 프로그램 (일반적으로 HTTP 요청 수), URL, 응답 시간 및 성공 또는 실패에 대 한 데이터를 사용 합니다.
* 종속성 - 앱이 실행한 REST 및 SQL 호출. URI, 응답 시간 및 성공 여부 포함
* 스택 추적을 포함한 예외.
* 페이지 보기 데이터 hello 사용자의 브라우저에서 제공 합니다.
* 성능 카운터 등의 메트릭과 직접 작성한 메트릭. 
* Tootrack 비즈니스 이벤트를 사용할 수 있는 사용자 지정 이벤트
* 디버깅에 사용하는 로그 추적.

## <a name="case-study-real-madrid-fc"></a>사례 연구: Real Madrid F.C.
웹 서비스의 hello [실제 마드리드 Football 클럽](http://www.realmadrid.com/) hello 전 세계 450 백만 약 팬 속도 제공 합니다. 팬 웹 브라우저를 통해 모두 액세스 하 고 hello 클럽의 모바일 응용 프로그램입니다. 팬은 입장권을 예매할 수 있을 뿐만 아니라 경기 결과, 선수, 예정 경기에 대한 정보와 비디오 클립에도 액세스할 수 있습니다. 골인 수 등의 필터로 검색도 가능합니다. 링크 toosocial 미디어도 있습니다. hello 사용자 환경이 매우 개인 설정 하 고 양방향 통신 tooengage 팬으로 설계 되었습니다.

솔루션을 hello [는 서비스 및 Microsoft Azure에서 응용 프로그램의 시스템](https://www.microsoft.com/en-us/enterprise/microsoftcloud/realmadrid.aspx)합니다. 확장성은 핵심 요구 사항입니다. 트래픽은 변동이 심하고 경기 무렵이나 도중에 매우 높아질 수 있습니다.

실제 마드리드는 중요 한 toomonitor hello 시스템 성능 Azure Application Insights 제공 hello 시스템 전체에서 안정적이 고 높은 수준의 서비스를 확인 합니다. 

hello 클럽 가져옵니다 해당 팬의 깊이 있게 이해:이 위치 (%3은 스페인), 플레이어, 기록 결과 및 예정 된 게임 및 toomatch 결과 응답 방식을에 있는 이자 합니다.

대부분의 원격 분석 데이터가이 hello 솔루션을 단순화 하 고 작업의 복잡성을 감소 하는 추가 코드 없이 자동으로 수집 됩니다.  Application Insights는 Real Madrid 대신 매달 38억 개의 원격 분석 지점을 처리합니다.

실제 마드리드 hello Power BI 모듈 tooview 해당 원격 분석을 사용합니다.

![Application Insights 원격 분석의 Power BI 보기](./media/app-insights-devops/080.png)

## <a name="smart-detection"></a>스마트 감지
[사전 진단](app-insights-proactive-diagnostics.md)은 최신 기능입니다. 사용자가 특별한 구성을 하지 않아도 Application Insights가 앱에서 실패율이 비정상적으로 증가하는 것을 자동으로 감지하고 알립니다. 정도로 스마트 tooignore 따른 실패의 배경을 이며 있는 상승 합니다.이 요청에서 tooa 많은 단순히 비례 하는 또한입니다. 예를 들어에 의존 하는 hello 서비스 중 하나에 오류가 있을 때 또는 hello 새 빌드 방금 배포한 경우 작동 하지 않습니다 에서도 완벽 하 게, 사용자의 전자 메일을 살펴보면으로 항목에 대 한 파악 한 다음. (또한 webhook가 있어 다른 앱을 트리거할 수 있습니다.)

이 기능의 또 다른 측면은 하드 toodiscover 성능의 특별 한 패턴을 찾고 있습니다. 원격 분석을 매일 심층 분석을 수행 합니다. 예를 들어, 특정 지리적 영역 또는 특정 브라우저 버전과 관련된 성능 저하 문제를 찾을 수 있습니다.

두 경우 모두 hello 경고를 검색 하는 현상 hello 하지만 또한 toohelp 필요한 데이터를 진단할 제공 hello 관련 예외 보고서와 같은 문제 뿐 아니라 알려 줍니다.

![사전 진단에서 전자 메일](./media/app-insights-devops/030.png)

Samtec 고객은 다음과 같이 말했습니다. "최근 기능 컷오버를 하면서 리소스 한도까지 올라가서 시간 초과를 발생시키는 축소된 데이터베이스를 발견했습니다. 자동 관리 검색 경고를 통해 들어온 알리는 근 실시간으로 매우 hello 문제 심사 된 것 처럼 리터럴로 합니다. Hello Azure 플랫폼 경고와 결합 되어이 경고는 거의 즉시 hello 문제를 해결 하는 데 도움을 준 합니다. 총 가동 중지 시간은 10분 미만이었습니다."

## <a name="live-metrics-stream"></a>라이브 메트릭 스트림
Hello 최신 빌드를 배포 합니다. 급하게 경험 될 수 있습니다. 문제가 경우 원하는 //office.microsoft.com/ tooknow 당장 필요한 경우 내용을 취소할 수 있도록 합니다. 라이브 메트릭 스트림은 약 1초의 대기 시간으로 주요 메트릭을 제공합니다.

![라이브 메트릭](./media/app-insights-devops/040.png)

즉시 모든 실패 또는 예외의 샘플을 검사할 수 있습니다.

![라이브 실패 이벤트](./media/app-insights-devops/live-stream-failures.png)

## <a name="application-map"></a>응용 프로그램 맵
응용 프로그램 맵을 자동으로 검색 응용 프로그램 토폴로지를 쉽게 분산된 환경에서 성능 병목 지점 및 문제가 있는 흐름을 식별할 toolet 그 위에 hello 성능 정보를 배치 합니다. 있습니다 toodiscover 응용 프로그램 종속성을 Azure 서비스에서. 코드와 관련 된 경우를 이해 하거나 종속성 관련 하 여 hello 문제 심사 하 고 관련 진단 한 곳에 드릴에서 발생할 수 있습니다. 예를 들어 SQL 계층 tooperformance 저하 인해 응용 프로그램에 문제가 있습니다. 응용 프로그램 맵을 사용 하 여 즉시 볼 수 있으며 hello SQL 인덱스 관리자 또는 쿼리 Insights 환경을 더 자세히 분석 키를 누릅니다.

![응용 프로그램 맵](./media/app-insights-devops/050.png)

## <a name="application-insights-analytics"></a>Application Insights Analytics
[Analytics](app-insights-analytics.md)를 사용하면 SQL과 유사한 강력한 언어로 임의의 쿼리를 작성할 수 있습니다.  다양 한 관점 연결 상태를 유지 하 고 hello 올바른 질문 toocorrelate 서비스 성능을 비즈니스 메트릭 및 고객 만족도 요청할 수 있습니다 hello 전체 앱 스택 간 진단 간편해 집니다. 

모든 원격 분석 인스턴스 및 hello 포털에 저장 된 메트릭 원시 데이터를 쿼리할 수 있습니다. hello 언어 필터, 조인, 집계 및 기타 작업을 포함합니다. 필드 계산과 통계 분석도 수행할 수 있습니다. 테이블 형식 및 그래픽 시각화가 모두 들어 있습니다.

![분석 쿼리 및 결과 차트](./media/app-insights-devops/025.png)

예를 들어, 다음과 같은 작업이 간편합니다.

* 성능 데이터를 고객 눈금 toounderstand 경험 하는 응용 프로그램의 요청을 분할 합니다.
* 라이브 사이트 검사 시 특정 오류 코드 또는 사용자 지정 이벤트 이름을 검색합니다.
* 드릴 다운 toounderstand 특정 고객의 hello 앱 사용 기능 획득 하 고 적용 되는 방법입니다.
* 세션 및 특정 사용자에 게 tooenable 지원 및 운영 팀 tooprovide 인스턴트 고객 지원에 대 한 응답 시간을 추적 합니다.
* 자주 사용 되는 앱 기능 tooanswer 기능 우선 순위 지정 질문을 결정 합니다.

고객 DNN 있다고: "Application Insights에서 제공한 toocombine 수, 정렬, 쿼리 및 필요에 따라 데이터를 필터링 하는 것에 대 한 hello 수식의 부분이 없습니다 hello로 합니다. 자신의 창의력 및 경험 toofind 우리 팀 toouse 허용 강력한 쿼리 언어를 사용 하 여 데이터 있었습니다 toofind insights 및 우리 미처 확인 했습니다. 문제를 해결 합니다. Hello 질문부터에서 흥미로운 답변을 많이 제공 *' I 불가사의 if...'.*"

## <a name="development-tools-integration"></a>개발 도구 통합
### <a name="configuring-application-insights"></a>Application Insights 구성
Visual Studio 및 Eclipse 개발 하는 hello 프로젝트에 대 한 도구 tooconfigure hello 올바른 SDK 패키지 있어야 합니다. 메뉴 명령 tooadd Application Insights 있습니다.

Toobe Log4N, NLog, 또는 System.Diagnostics.Trace와 같은 추적 로깅 프레임 워크를 사용 하 여 발생 하는 경우 다음 얻게 hello 함께 hello 옵션 toosend hello 로그 tooApplication Insights 다른 원격 분석을 요청과 함께 hello 추적 쉽게 연관 시킬 수 있습니다. 종속성 호출 및 예외입니다.

### <a name="search-telemetry-in-visual-studio"></a>Visual Studio에서 원격 분석 검색
개발 및 디버깅 기능을 볼 수 있으며 검색 hello hello hello 웹 포털에서 기능으로 동일한 검색을 사용 하 여 Visual Studio에서 직접 원격 분석 합니다.

및 Visual Studio에서 hello 데이터 요소를 볼 수 있으며 직선 toohello 관련 코드를 이동할 때 Application Insights 예외를 기록 합니다.

![Visual Studio 검색](./media/app-insights-devops/060.png)

디버깅 중 hello 옵션 tookeep hello 원격 분석에에서 있는 개발 컴퓨터, Visual Studio에서 있지만 toohello 포털을 보내지 않고 보기. 이 로컬 옵션은 디버깅과 프로덕션 원격 분석이 섞이지 않도록 방지합니다.

### <a name="build-annotations"></a>빌드 주석
Visual Studio Team Services toobuild를 사용 하 여 앱을 배포 하는 경우 배포 주석 hello 포털에서 차트에 표시 합니다. 최신 릴리스 hello 기준에 영향을 줄이 있으면 알 수 있습니다.

![빌드 주석](./media/app-insights-devops/070.png)

### <a name="work-items"></a>작업 항목
경고가 발생한 경우 Application Insights는 자동으로 사용자의 작업 추적 시스템에서 작업 항목을 만듭니다.

## <a name="but-what-about"></a>기타 사항
* [개인 정보 보호 및 저장소](app-insights-data-retention-privacy.md) - 원격 분석은 Azure 보안 서버에 보관됩니다.
* 성능-hello 영향 매우 낮습니다. 원격 분석은 일괄 처리됩니다.
* [가격 책정](app-insights-pricing.md) - 무료로 시작할 수 있고 낮은 볼륨에서는 계속 무료로 이용할 수 있습니다.


## <a name="video"></a>비디오

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>다음 단계
Application Insights로 시작하기가 쉽습니다. hello 기본 옵션이 있습니다.

* 이미 실행 중인 웹앱을 계측합니다. 이 모든 hello에 대 한 기본 제공 성능 원격 분석을 제공합니다. [Java](app-insights-java-live.md), [IIS 서버](app-insights-monitor-performance-live-website-now.md) 및 [Azure Web Apps](app-insights-azure.md)에서 사용할 수 있습니다.
* 개발 중에 프로젝트를 계측합니다. [ASP.NET](app-insights-asp-net.md) 또는 [Java](app-insights-java-get-started.md) 앱, [Node.js](app-insights-nodejs.md), 여러 가지 [기타 유형](app-insights-platforms.md) 호스트에 적용할 수 있습니다. 
* 짧은 코드 조각을 추가하여 [아무 웹 페이지](app-insights-javascript.md) 나 계측합니다.

