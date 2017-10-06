---
title: "aaaData 보존 및 저장소 Azure Application Insights에서 | Microsoft Docs"
description: "보존 및 개인 정보 취급 방침"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Application Insights 데이터 수집, 보존 및 저장소


설치 하는 경우 [Azure Application Insights] [ start] 앱에서 SDK, 앱 toohello 클라우드 사용자에 대 한 원격 분석 전송 합니다. 당연히 책임 개발자 원하는 tooknow 정확 하 게 전송 되는 데이터, 어떤 일이 생기 toohello 데이터 및 방법을 제어를 유지할 수 있습니다. 특히 중요한 데이터를 보낼 수 있는지, 저장되었는지 및 얼마나 안전한지를 파악합니다. 

첫째, hello 자동 검색:

* "hello 초기"를 실행 하는 hello 표준 원격 분석 모듈에는 중요 한 데이터 toohello 서비스으 나 가능성이 toosend은입니다. hello 원격 분석 부하, 성능 및 사용 메트릭을, 예외 보고서 및 기타 진단 데이터와 관련 되어 있습니다. hello 진단 보고서에 표시 되는 hello 기본 사용자 데이터는 Url입니다. 하지만 앱 URL에 일반 텍스트에 중요 한 데이터를 어떤 경우에 포함 해서는 안 합니다.
* 추가 사용자 지정 원격 분석 toohelp 보내는 코드를 작성할 수 있는 진단 및 사용 현황 모니터링 합니다. (이 확장성은 Application Insights의 매우 유용한 기능입니다.) 실수, toowrite 개인 포함 되도록이 코드 및 기타 중요 한 데이터를 통해서는 가능 됩니다. 응용 프로그램이 해당 데이터와 함께 작동 하는 경우 작성 하는 철저 한 검토 프로세스 tooall hello 코드를 적용 해야 합니다.
* 개발 하 고 앱을 테스트 하는 동안 것이 쉬운 tooinspect hello SDK에서 전송 되는 기능입니다. hello 데이터 hello 디버깅 IDE hello 및 브라우저의 출력 창에에서 나타납니다. 
* hello 데이터에 보유 되므로 [Microsoft Azure](http://azure.com) hello 미국 또는 유럽의 서버입니다. 그러나 앱은 어디서나 실행할 수 있습니다. Azure는 [강력한 보안 프로세스를 가지고 광범위한 규정 준수 표준을 충족](https://azure.microsoft.com/support/trust-center/)합니다. 만 지정 된 팀과 tooyour 데이터에 액세스 했습니다. Microsoft 직원 지식와 특정 제한 된 경우에만 액세스 tooit을 제한 될 수 있습니다. Hello 서버에 없는 경우에 전송 중에 암호화 됩니다.

이 문서의 나머지 부분 hello 보다 완전 하 게 이러한 응답을 설명 합니다. 그는 디자인 toobe 자체 포함 된 toocolleagues 소속 팀의 일부가 아닌 사용자를 표시할 수 있습니다.

## <a name="what-is-application-insights"></a>Application Insights란?
[Azure Application Insights] [ start] 때 도움이 되는 Microsoft에서 제공 하는 서비스는 hello 성능 및 라이브 응용 프로그램의 유용성 향상 됩니다. 응용 프로그램 테스트 및 게시 하거나 배포 된 후 실행 중인 모든 hello 시간을 모니터링 합니다. 예를 들어 있는 시간을 대부분의 사용자가 가져올 응답 hello 앱이 되는 서비스는 올바른 외부에서 제공 하는 방법 등에 종속에 application Insights를 보여 주는 테이블과 차트를 만듭니다. 충돌, 오류 또는 성능 문제가 있는 경우에 세부 toodiagnose hello 원인에서 hello 원격 분석 데이터를 통해 검색할 수 있습니다. 및 hello 서비스 사용자에 게 전자 메일 앱의 hello 가용성과 성능을에 변경 된 경우.

Tooget 순서에서에서이 기능을 설치한 Application Insights SDK에서 응용 프로그램 코드의 일부가 되 합니다. 앱이 실행 되는 경우 hello SDK는 해당 작업을 모니터링 하 고 toohello Application Insights 원격 분석 서비스를 보냅니다. [Microsoft Azure](http://azure.com)에서 호스팅하는 클라우드 서비스입니다. (하지만 Application Insights는 Azure에서 호스팅되는 서비스가 아닌 모든 응용 프로그램에 대해 작동합니다.)

![응용 프로그램에 hello SDK 원격 분석 toohello Application Insights 서비스를 보냅니다.](./media/app-insights-data-retention-privacy/01-scheme.png)

hello Application Insights 서비스를 저장 하 고 hello 원격 분석을 분석 합니다. toosee hello 분석 또는 hello 통해 검색은 원격 분석을 저장 응용 프로그램에 대 한 Azure 계정 tooyour 및 열기 hello Application Insights 리소스에 로그인 합니다. 하거나 수도 있습니다 공유 toohello 데이터를 액세스 팀의 다른 멤버와 지정 된 Azure 구독자가 있는 합니다.

Hello Application Insights 서비스에서에서 내보낸 데이터를 가질 수 있습니다 예 tooa 데이터베이스나 tooexternal 도구입니다. Hello 서비스에서 가져오는 특수 한 키를 가진 각 도구를 제공 합니다. 필요한 경우 hello 키를 해지할 수 있습니다. 

Application Insights Sdk 응용 프로그램 종류의 범위에 사용할 수 있는: 사용자 고유의 J2EE 또는 ASP.NET 서버 또는 Azure; 호스팅된 웹 서비스 웹 클라이언트-즉, 웹 페이지;에서 실행 하는 hello 코드 데스크톱 응용 프로그램 및 서비스 Windows Phone, iOS 및 Android와 같은 장치 앱입니다. 원격 분석 toohello 보내는 동일한 서비스입니다.

## <a name="what-data-does-it-collect"></a>어떤 데이터를 수집하나요?
### <a name="how-is-hello-data-is-collected"></a>어떻게는 hello 데이터를 수집 하나요?
세 가지 데이터 원본이 있습니다.

* hello 하거나 앱과 통합 하는 SDK [개발에서](app-insights-asp-net.md) 또는 [런타임 시](app-insights-monitor-performance-live-website-now.md)합니다. 다른 응용 프로그램 형식에 대한 여러 SDK가 있습니다. 또한는 [웹 페이지에 대 한 SDK](app-insights-javascript.md), hello 페이지와 함께 hello 최종 사용자의 브라우저에 로드 합니다.
  
  * 각 SDK에는 수의 [모듈](app-insights-configuration-with-applicationinsights-config.md), 다양 한 기술을 toocollect 다양 한 유형의 원격 분석을 사용 하는 합니다.
  * 개발에서 hello SDK를 설치 하는 경우 사용할 수 있습니다 해당 API toosend 직접 원격 분석 추가 toohello 기본 모듈에서. 이 사용자 지정 원격 분석 toosend 데이터를 포함할 수 있습니다.
* 일부 웹 서버에 CPU, 메모리 및 네트워크 선점 하는 방법에 대 한 원격 분석 hello 응용 프로그램과 함께 실행 하는 에이전트도 있습니다. 예를 들어 Azure VM, Docker 호스트 및 [J2EE 서버](app-insights-java-agent.md) 에는 이러한 에이전트가 있을 수 있습니다.
* [가용성 테스트](app-insights-monitor-web-app-availability.md) 보낼 요청 tooyour 웹 앱을 정기적으로 Microsoft에 의해 프로세스가 실행 됩니다. hello 결과 toohello Application Insights 서비스에 전송 됩니다.

### <a name="what-kinds-of-data-are-collected"></a>어떤 종류의 데이터를 수집하나요?
hello 주요 범주는 있습니다.

* [웹 서버 원격 분석](app-insights-asp-net.md) - HTTP가 요청합니다.  Uri에 걸린 시간 tooprocess hello 요청, 응답 코드, 클라이언트 IP 주소입니다. 세션 ID.
* [웹 페이지](app-insights-javascript.md) -페이지, 사용자 및 세션 수입니다. 페이지 로드 시간. 예외. Ajax 호출.
* 성능 카운터 - 메모리, CPU, IO, 네트워크 선점입니다.
* 클라이언트 및 서버 컨텍스트 - OS, 로캘, 장치 형식, 브라우저, 화면 해상도입니다.
* [예외](app-insights-asp-net-exceptions.md) 및 작동 중단 - **스택 덤프**, 작성 ID, CPU 형식입니다. 
* [종속성](app-insights-asp-net-dependencies.md) -REST, SQL, AJAX 등 tooexternal 서비스를 호출 합니다. URI 또는 연결 문자열, 시간, 성공, 명령입니다.
* [가용성 테스트](app-insights-monitor-web-app-availability.md) - 테스트, 단계, 응답의 기간입니다.
* [추적 로그](app-insights-asp-net-trace-logs.md) 및 [사용자 지정 원격 분석](app-insights-api-custom-events-metrics.md) - **로그 또는 원격 분석에 코딩한 것**입니다.

[자세한 내용](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>수집되는 항목을 어떻게 확인할 수 있나요?
Visual Studio를 사용 하 여 hello 앱을 개발 하는 경우 디버그 모드 (F5) hello 앱을 실행 합니다. hello 원격 분석 hello 출력 창에 나타납니다. 여기에서 복사하고 쉬운 검사를 JSON으로 형식으로 지정할 수 있습니다. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

Hello 진단 창에 보다 읽기 쉬운 보기도 됩니다.

웹 페이지의 경우 브라우저의 디버깅 창을 엽니다.

![F12 키를 누릅니다 하 고 hello 네트워크 탭을 엽니다.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>작성할 수 있습니까 코드 toofilter hello 원격 분석 전송 하기 전에?
[원격 분석 프로세서 플러그 인](app-insights-api-filtering-sampling.md)을 작성하여 수행할 수 있습니다.

## <a name="how-long-is-hello-data-kept"></a>시간 보관 하는 hello 데이터?
원시 데이터 요소 (즉, 분석에서 쿼리할 검색에서 검사할 수 있는 항목)에 대 한 일 수를 보관 됩니다. 이보다 긴 tookeep 데이터, 필요한 경우 사용할 수 있습니다 [연속 내보내기를](app-insights-export-telemetry.md) toocopy 것 tooa 저장소 계정입니다.

집계 데이터(즉, 메트릭 탐색기에 표시되는 개수, 평균 및 기타 통계 데이터)는 90일 동안 1분 단위로 보존됩니다.

## <a name="who-can-access-hello-data"></a>Hello 데이터에 액세스할 수 있는 사용자?
hello 데이터는 tooyou 표시 되 고, 팀 구성원에 게 조직 계정이 있는 경우. 

플랫폼 복사한 tooother 위치 수 있으며와 팀 구성원이로 내보낼 수 tooother 사람들에 전달 합니다.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>Microsoft는 hello 정보로이 응용 프로그램 tooApplication Insights 보냅니다?
Microsoft 순서 tooprovide hello 서비스 tooyou 에서만에서 hello 데이터를 사용합니다.

## <a name="where-is-hello-data-held"></a>Hello 데이터 커서가?
* hello 미국 또는 유럽입니다. 새 Application Insights 리소스를 만들 때 hello 위치를 선택할 수 있습니다. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>내 응용 프로그램에 hello 미국 또는 유럽에서에서 호스팅되는 toobe 의미 입니까?
* 아니요. 응용 프로그램는 자신의 온-프레미스 호스트 또는 클라우드 hello 어디에서 나 실행할 수 있습니다.

## <a name="how-secure-is-my-data"></a>내 데이터는 어느 정도 안전한가요?
Application Insights는 Azure 서비스입니다. 보안 정책은 hello에 설명 된 [Azure 보안, 개인 정보 보호 및 규정 준수 백서](http://go.microsoft.com/fwlink/?linkid=392408)합니다.

hello 데이터는 Microsoft Azure 서버에 저장 됩니다. Hello Azure 포털에서에서 계정에 대 한 계정 제한 사항 hello에 설명 된 [Azure 보안, 개인 정보 보호 및 규정 준수 문서](http://go.microsoft.com/fwlink/?linkid=392408)합니다.

Microsoft 담당자가 tooyour 데이터 액세스 제한 되어 있습니다. 권한만 사용 하 여 데이터에 액세스할 있습니다 경우 필요한 toosupport 사용자의 사용 및 Application Insights 합니다. 

모든 고객의 응용 프로그램 (예: 데이터 속도 추적의 평균 크기) 전체에서 집계의 데이터에 사용 되는 tooimprove Application Insights입니다.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>다른 사람의 원격 분석이 내 Application Insights 데이터에 방해가 될 수 있나요?
웹 페이지의 hello 코드에서 찾을 수 있는 hello 계측 키를 사용 하 여 원격 분석 추가 tooyour 계정을 보낼 수 없습니다. 추가 데이터가 충분하면 메트릭이 앱의 성능 및 사용을 올바르게 나타냅니다.

다른 프로젝트와 코드를 공유 하는 경우 tooremove 계측 키를 기억 합니다.

## <a name="is-hello-data-encrypted"></a>Hello 데이터 암호화
현재 서버 hello 포함 되어 있지 않습니다.

모든 데이터는 데이터 센터 간에 이동할 때 암호화됩니다.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>내 응용 프로그램 tooApplication Insights 서버에서 전송 중에 암호화 된 hello 데이터?
예, https toosend 데이터 toohello 포털에서 웹 서버, 장치 및 HTTPS 웹 페이지 등 거의 모든 Sdk 사용 합니다. hello 유일한 예외는 일반 HTTP 웹 페이지에서 보낸 데이터입니다. 

## <a name="personally-identifiable-information"></a>개인 식별이 가능한 정보
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>개인 식별이 가능한 정보 (PII)를 보낼 수 tooApplication Insights?
예, 전송할 수 있습니다. 

일반 지침:

* 대부분의 표준 원격 분석(즉, 코드를 작성하지 않고 전송된 원격 분석)은 명시적 PII를 포함하지 않습니다. 그러나 이벤트의 컬렉션에서 유추 하 여 가능한 tooidentify 개인 수도 있습니다.
* 예외 및 추적 메시지는 PII를 포함할 수 있습니다.
* 사용자 지정 원격 분석-TrackEvent hello API 또는 로그 추적을 사용 하 여 코드를 작성 하는 등 호출-선택한 모든 데이터를 포함할 수 있습니다.

hello hello 끝이 문서에 표에서 hello 데이터 수집에 대해 더 자세히 설명 합니다.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>법률 및 큰지에 tooPII에 규정을 준수 합니까?
예. Hello 데이터의 hello 수집 및 사용 hello Microsoft 온라인 서비스 약관 및 법률 및 규정을 준수 하 여 책임 tooensure 이며

에 게 알려야 고객이 적절 하 게 hello 데이터를 수집 하는 응용 프로그램 및 hello 데이터 사용 방법에 대 한 합니다.

#### <a name="can-my-users-turn-off-application-insights"></a>내 사용자가 Application Insights를 끌 수 있나요?
직접 끌 수는 없습니다. 스위치를 제공 하지 않는 사용자가 Application Insights 오프 tooturn를 작동할 수 있습니다.

그러나 응용 프로그램에서 이러한 기능을 구현할 수 있습니다. 모든 hello Sdk 원격 분석 수집을 해제 하는 API 설정이 포함 됩니다. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>내 응용 프로그램이 의도하지 않게 중요한 정보를 수집하고 있습니다. Application Insights에서 이 데이터가 보존되지 않도록 삭제할 수 있나요?
Application Insights는 데이터를 필터링하거나 삭제하지 않습니다. Hello 데이터를 적절 하 게 관리 하 고 이러한 데이터 tooApplication Insights 전송 하지 않도록 해야 합니다.

## <a name="data-sent-by-application-insights"></a>Application Insights에서 보내는 데이터
hello Sdk 플랫폼 간에 변경 하 고 설치할 수 있는 구성 요소에 는지 않습니다. (너무 참조[Application Insights-개요][start].) 각 구성 요소마다 다른 데이터를 보냅니다.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>다양한 시나리오에서 전송되는 데이터 클래스
| 사용자 작업 | 수집되는 데이터 클래스(다음 표 참조) |
| --- | --- |
| [Application Insights SDK tooa.NET 웹 프로젝트에 추가][greenbrown] |ServerContext<br/>유추<br/>성능 카운터<br/>요청<br/>**예외**<br/>세션<br/>users |
| [IIS에서 상태 모니터 설치][redfield] |종속성<br/>ServerContext<br/>유추<br/>성능 카운터 |
| [Application Insights SDK tooa Java 웹 응용 프로그램 추가][java] |ServerContext<br/>유추<br/>요청<br/>세션<br/>users |
| [JavaScript SDK tooweb 페이지 추가][client] |ClientContext  <br/>유추<br/>Page<br/>ClientPerf<br/>Ajax |
| [기본 속성 정의][apiproperties] |**속성**  |
| [호출 TrackMetric][api] |숫자 값<br/>**속성** |
| [호출 추적*][api] |이벤트 이름<br/>**속성** |
| [호출 TrackException][api] |**예외**<br/>스택 덤프<br/>**속성** |
| SDK는 데이터를 수집할 수 없습니다. 예: <br/> - 성능 카운터에 액세스할 수 없음<br/> - 원격 분석 이니셜라이저 예외 |SDK 진단 |

[다른 플랫폼에 대한 SDK][platforms]의 경우 해당 문서를 참조하세요.

#### <a name="hello-classes-of-collected-data"></a>수집 된 데이터의 hello 클래스
| 수집되는 데이터 클래스 | 포함(전체 목록 아님) |
| --- | --- |
| **속성** |**임의 데이터 - 코드에 의해 결정됨** |
| DeviceContext |ID, IP, 로캘, 장치 모델, 네트워크, 네트워크 종류, OEM 이름, 화면 해상도, 역할 인스턴스, 역할 이름, 장치 유형 |
| ClientContext  |OS, 로캘, 언어, 네트워크, 창 해상도 |
| 세션 |세션 ID |
| ServerContext |컴퓨터 이름, 로캘, OS, 장치, 사용자 세션, 사용자 컨텍스트, 작업 |
| 유추 |IP 주소, 타임스탬프, OS, 브라우저에서 지리적 위치 유추 |
| 메트릭 |메트릭 이름 및 값 |
| 이벤트 |이벤트 이름 및 값 |
| PageViews |URL 및 페이지 이름이나 화면 이름 |
| 클라이언트 성능 |URL/페이지 이름, 브라우저 로드 시간 |
| Ajax |웹 페이지 tooserver에서 HTTP 호출 |
| 요청 |URL, 기간, 응답 코드 |
| 종속성 |유형(SQL, HTTP,...), 연결 문자열 또는 URI, 동기/비동기, 기간, 성공, SQL 문(상태 모니터 사용) |
| **예외** |유형, **메시지**, 호출 스택, 원본 파일 및 줄 번호, 스레드 ID |
| 충돌 |프로세스 ID, 부모 프로세스 ID, 충돌 스레드 ID; 응용 프로그램 패치, ID, 빌드; 예외 유형, 주소, 이유; 난독 처리된 기호 및 레지스터, 이진 시작 및 끝 주소, 이진 이름 및 경로, CPU 종류 |
| 추적 |**메시지** 및 심각도 수준 |
| 성능 카운터 |프로세서 시간, 사용 가능한 메모리, 요청 속도, 예외 속도, 프로세스 전용 바이트, IO 속도, 요청 기간, 요청 큐 길이 |
| Availability |웹 테스트 응답 코드, 각 테스트 단계, 테스트 이름, 타임 스탬프, 성공, 응답 시간, 테스트 위치의 기간 |
| SDK 진단 |추적 메시지 또는 예외 |

있습니다 수 [ApplicationInsights.config를 편집 하 여 hello 데이터 중 일부를 전환 합니다.][config]

## <a name="credits"></a>크레딧
이 제품에는 MaxMind에서 작성된 GeoLite2 데이터를 포함하며 [http://www.maxmind.com](http://www.maxmind.com)에 있습니다.



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

