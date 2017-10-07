---
title: "aaaTroubleshooting 데이터가 없는-.NET 용 Application Insights"
description: "Azure Application Insights에서 데이터를 볼 수 없나요? 여기를 참조하세요."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>데이터 없음 문제 해결 - .NET용 Application Insights
## <a name="some-of-my-telemetry-is-missing"></a>일부 원격 분석이 누락됨
*Application Insights에서만 응용 프로그램에서 생성 하는 hello 이벤트의 분수를 참조 합니다.*

* 일관 되 게 표시 되는 경우 동일한 hello 분수, 아마도 due tooadaptive [샘플링](app-insights-sampling.md)합니다. tooconfirm이를 검색 (에서 hello 개요 블레이드에)를 연 요청 또는 기타 이벤트의 인스턴스를 확인 합니다. Hello hello 속성 섹션 맨 아래에 "..." tooget 전체 속성 자세히를 클릭 합니다. 요청 수가 1보다 크면 샘플링이 작동 중인 것입니다. 
* 그렇지 않은 경우 요금제의 [데이터 속도 제한](app-insights-pricing.md#limits-summary) 에 도달한 것일 수 있습니다. 이러한 제한은 분당으로 적용됩니다.

## <a name="no-data-from-my-server"></a>내 서버에서 데이터 없음
*웹 서버에 이 앱을 설치했지만 지금 원격 분석이 표시되지 않습니다. 내 개발 컴퓨터에서 문제 없이 작동했습니다.*

* 아마도 방화벽 문제일 것입니다. [Application Insights toosend 데이터에 대 한 방화벽 예외 설정](app-insights-ip-addresses.md)합니다.

*I [상태 모니터 설치](app-insights-monitor-performance-live-website-now.md) 웹 서버 toomonitor 기존 응용 프로그램에 있습니다. 결과가 보이지 않습니다.*

* [상태 모니터 문제 해결](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)을 참조하세요. 

## <a name="q01"></a>Visual Studio에 'Application Insights 추가' 옵션이 없음
*Solution Explorer에서 기존 프로젝트를 마우스 오른쪽 단추로 클릭할 때 Application Insights 옵션이 표시되지 않습니다.*

* 일부 유형의.NET 프로젝트는 hello 도구에서 지원 됩니다. 웹 및 WCF 프로젝트는 지원됩니다. 데스크톱 또는 서비스 응용 프로그램과 같은 다른 프로젝트 형식에 여전히 [Application Insights SDK tooyour 프로젝트를 수동으로 추가](app-insights-windows-desktop.md)합니다.
* [Visual Studio 2013 업데이트 3 이후](http://go.microsoft.com/fwlink/?LinkId=397827)가 설치되어 있는지 확인하세요. 사전 설치 된 hello Application Insights SDK를 제공 하는 개발자 분석 도구와 함께 제공 됩니다.
* **도구**, **확장 및 업데이트**를 차례로 선택하고 **개발자 분석 도구**가 설치 및 활성화되었는지 확인하세요. 그렇다면, **업데이트** toosee 경우 한 업데이트가 제공 됩니다.
* Hello 새 프로젝트 대화 상자를 열고 ASP.NET 웹 응용 프로그램을 선택 합니다. 나타날 경우 Application Insights 옵션, hello 하면 hello 도구가 설치 됩니다. 그렇지 않은 경우을 제거한 다음 다시 hello Application Insights Tools를 설치 해 보십시오.

## <a name="q02"></a>Application Insights 추가 실패
*를 할 때 tooadd Application Insights tooan 기존 프로젝트 오류 메시지가 나타납니다.*

가능한 원인:

* Application Insights 포털 hello와 통신 하지 못했습니다. 또는
* Azure 계정에 문제가 있습니다.
* 하기만 하면 [toohello 구독 읽기 권한 또는 그룹 toocreate hello 새 리소스 하려던](app-insights-resources-roles-access-control.md)합니다.

해결 방법:

* Hello 오른쪽 Azure 계정에 대 한 로그인 자격 증명을 입력 했는지 확인 하십시오. 
* 브라우저에서 확인 해야 하는 액세스 toohello [Azure 포털](https://portal.azure.com)합니다. 설정을 열고 제한이 있는지 확인합니다.
* [Application Insights tooyour 기존 프로젝트 추가](app-insights-asp-net.md): 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 "Application Insights를 추가 합니다."를 선택 합니다.
* 아직 작동 하지 않는 경우에 따라 hello [수동 절차](app-insights-windows-services.md) tooadd hello 포털에서 리소스 다음 hello SDK tooyour 프로젝트를 추가 합니다. 

## <a name="emptykey"></a>"계측 키는 비워 둘 수 없습니다." 오류가 발생합니다.
Application Insights를 설치하는 동안 문제가 발생했거나 로깅 어댑터에 문제가 있을 수 있습니다.

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **Application Insights > Application Insights 구성**을 차례로 선택합니다. TooAzure 안에 toosign 초대 하는 대화 상자를 얻을 수 및 Application Insights 리소스를 만들거나 기존 집합을 다시 사용 하거나 합니다.

## <a name="NuGetBuild"></a> 빌드 서버에 "NuGet 패키지가 없음"
*모든 빌드 내 개발 컴퓨터에서 디버깅 중인 I 하지만 오류가 표시 됨 NuGet hello 빌드 서버에서 확인 합니다.*

[NuGet 패키지 복원](http://docs.nuget.org/Consume/Package-Restore) 및 [자동 패키지 복원](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore)을 참조하세요.

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>누락 된 메뉴 명령 tooopen Visual Studio에서 Application Insights
*프로젝트 솔루션 탐색기를 마우스 오른쪽 단추로 클릭해도 Application Insights 명령 또는 Application Insights 열기 명령이 보이지 않습니다.*

가능한 원인:

* Hello Application Insights 리소스를 수동으로 만든 또는 hello 프로젝트는 hello Application Insights 도구에서 지원 되지 않는 형식입니다.
* hello 개발자 분석 도구는 Visual Studio에서 사용할 수 없습니다. 
* Visual Studio 버전이 2013 업데이트 3보다 오래되었습니다.

해결 방법:

* Visual Studio가 2013 업데이트 3 이상 버전인지 확인하세요.
* **도구**, **확장 및 업데이트**를 차례로 선택하고 **개발자 분석 도구**가 설치 및 활성화되었는지 확인하세요. 그렇다면, **업데이트** toosee 경우 한 업데이트가 제공 됩니다.
* 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다. Hello 명령이 표시 **Application Insights > Configure Application Insights**, tooconnect 사용 hello Application Insights 서비스에서에서 프로젝트 toohello 리소스입니다.

그렇지 않으면 프로젝트 형식은 hello Application Insights 도구에서 직접 지원 되지 않습니다. toosee toohello 로그인 하면 원격 분석 [Azure 포털](https://portal.azure.com)hello 왼쪽된 탐색 모음에서 Application Insights를 선택 하 고 응용 프로그램을 선택 합니다.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>Visual Studio에서 Application Insights를 열면 '액세스 거부' 오류
*hello ' Application Insights 열기 ' 메뉴 명령이 나 toohello Azure 포털 걸리지만 '액세스 거부' 오류 메시지가 나타나면.*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Microsoft 로그인 기본 브라우저에서 마지막으로 사용 하는 hello 액세스할 수 없는 너무[Application Insights toothis 앱 추가 되었을 때 만든 리소스가 hello](app-insights-asp-net.md)합니다. 가능한 원인은 두 가지입니다. 

* क ा ं Microsoft ख-작업과 개인 Microsoft 계정 미정 있습니까? hello 로그인 기본 브라우저에서 마지막으로 사용 하는 다른 계정에 대 한 hello 너무 액세스할 수 있는 하나 보다[toohello 프로젝트를 Application Insights 추가](app-insights-asp-net.md)합니다. 
  
  * Fix:에 있는 사용자 이름을 클릭 하 hello 브라우저 창의 오른쪽 위에 / 로그 아웃 합니다. 다음 액세스 권한이 있는 hello 계정으로 로그인 합니다. 그런 다음 hello 왼쪽된 탐색 모음에서 Application Insights를 클릭 하 고 앱을 선택 합니다.
* Application Insights toohello 프로젝트를 추가 하는 다른 사용자와 toogive 잊은 있습니다 [액세스 toohello 리소스 그룹](app-insights-resources-roles-access-control.md) 가 만들어진에 있습니다. 
  
  * Fix: 조직 계정을 사용 추가할 수 있습니다 toohello 팀; 또는 하면 개별 액세스 toohello 리소스 그룹에 부여할 수 있습니다.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>Visual Studio에서 Application Insights를 열면 '자산을 찾을 수 없음' 오류
*hello ' Application Insights 열기 ' 메뉴 명령이 나 toohello Azure 포털 걸리지만 '자산 파일을 찾을 수 없음' 오류 메시지가 나타나면.*

가능한 원인:

* hello 응용 프로그램에 대 한 Application Insights 리소스 삭제 되었습니다. 또는
* hello 계측 키 설정 되었거나 ApplicationInsights.config hello 프로젝트 파일을 업데이트 하지 않고 직접 편집 하 여 변경 합니다. 

hello hello 원격 분석 전송 대상 ApplicationInsights.config 컨트롤의 계측 키입니다. Hello 프로젝트 파일의 선을 hello 명령을 사용 하 여 Visual Studio에서 리소스를 열을 제어 합니다. 

해결 방법:

* 솔루션 탐색기 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Application Insights에 Application Insights 구성를 선택 합니다. Hello 대화 상자에서 toosend 원격 분석 tooan 기존 리소스를 선택 하거나 새로 만듭니다. 또는
* Hello 리소스를 직접 엽니다. 역시 로그인[Azure 포털 hello](https://portal.azure.com), hello 왼쪽된 탐색 모음에서 Application Insights를 클릭 한 다음 앱을 선택 합니다.

## <a name="where-do-i-find-my-telemetry"></a>내 원격 분석은 어디서 찾을 수 있습니까?
*사인 한 toohello [Microsoft Azure 포털](https://portal.azure.com), hello Azure 홈 대시보드 보고 하 고 있습니다. 내 Application Insights 데이터는 어디서 찾나요?*

* Hello 왼쪽된 탐색 모음에서 Application Insights를 응용 프로그램 이름에 다음을 클릭 합니다. 를 설정 하지 않은 모든 프로젝트 있을 경우 너무[추가 하거나 웹 프로젝트에서 Application Insights 구성](app-insights-asp-net.md)합니다.
  
    요약 차트 몇 개가 보일 것입니다. 통해 클릭할 수 있는 toosee 더 자세히 설명 합니다.
* Visual Studio에서 앱을 디버깅 하는 동안 hello Application Insights 단추를 클릭 합니다.

## <a name="q03"></a> 서버 데이터 없음(데이터가 하나도 없음)
*모든 hello 차트 표시 되지만 응용 프로그램을 실행 했으며 Microsoft Azure의 hello Application Insights 서비스를 연 다음 ' 학습 방법을 toocollect...' 또는 '구성 되지 않았습니다.'* 또는 *페이지 보기와 사용자 데이터만 표시되고 서버 데이터는 표시되지 않습니다.*

* Visual Studio의 디버그 모드에서 응용 프로그램을 실행합니다(F5). Hello 응용 프로그램을 사용 하므로 toogenerate로 일부 원격 분석 합니다. Hello Visual Studio 출력 창에 기록 된 이벤트를 볼 수 있는지 확인 합니다. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* Hello Application Insights 포털에서 엽니다 [진단 검색](app-insights-diagnostic-search.md)합니다. 일반적으로 데이터는 여기에 처음으로 나타납니다.
* Hello 새로 고침 단추를 클릭 합니다. hello 블레이드를 새로 고칩니다 자체 정기적으로, 있지만 수동으로도 수행할 수 있습니다. hello 새로 고침 간격은 더 큰 시간 범위에 대해 긴 경우
* Hello 계측 키가 일치를 확인 합니다. Hello에 hello Application Insights 포털에서 앱에 대 한 hello 주 블레이드에서 **Essentials** 드롭다운 목록에서 보면 **계측 키**합니다. 그런 다음 Visual Studio에서 프로젝트에서 ApplicationInsights.config 열고 hello `<instrumentationkey>`합니다. Hello 두 키가 같은지 확인 합니다. 같이 않으면
  
  * Hello 포털에서 Application Insights를 클릭 하 고 hello 오른쪽 키; hello 응용 프로그램 리소스에 대 한 확인 또는
  * Visual Studio 솔루션 탐색기 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 Application Insights을 구성을 선택 합니다. Hello 응용 프로그램 toosend 원격 분석 toohello 오른쪽 리소스를 다시 설정 합니다.
  * 사용 중인 검사 hello 동일 hello 일치 하는 키를 찾을 수 없는 경우 로그인 자격 증명 Visual Studio에서 toohello 포털에서와 같이 합니다.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* Hello에 [Microsoft Azure 홈 대시보드](https://portal.azure.com), hello 서비스 상태 맵을 살펴봅니다. 경고 설명 인은 tooOK 반환한을 Application Insights 응용 프로그램 블레이드를 다시 열 때까지 기다립니다.
* 또한 [상태 블로그](http://blogs.msdn.com/b/applicationinsights-status/)를 확인합니다.
* Hello에 대 한 코드 작성 [서버 쪽 SDK](app-insights-api-custom-events-metrics.md) 의 hello 계측 키 변경 될 수 있는 `TelemetryClient` 인스턴스 또는 `TelemetryContext`? 또는 너무 촘촘하게 걸러내는 [필터 또는 샘플링 구성](app-insights-api-filtering-sampling.md)을 작성했습니까?
* ApplicationInsights.config을 편집한 경우 신중 하 게 hello의 구성을 확인 [TelemetryInitializers 및 TelemetryProcessors](app-insights-api-filtering-sampling.md)합니다. 이름이 잘못 지정 된 형식 또는 매개 변수는 hello SDK toosend 데이터가 없는 발생할 수 있습니다.

## <a name="q04"></a>페이지 보기, 브라우저, 사용량에 데이터 없음
*페이지 보기 로드 시간에 또는 hello 브라우저 또는 사용량 블레이드에 데이터가 아니라 서버 응답 시간, 서버 요청 수 차트의 데이터를 표시 합니다.*

hello 데이터 hello 웹 페이지의 스크립트에서 제공 됩니다. 

* Application Insights tooan 기존 웹 프로젝트를 추가한 경우 [tooadd hello 스크립트를 직접 사용할](app-insights-javascript.md)합니다.
* Internet Explorer가 호환성 모드에서 사이트를 표시하고 있는지 확인합니다.
* Hello 브라우저의 디버그 기능 (일부 브라우저에서 f12 키를 눌러 네트워크)를 사용 하 여 데이터가 너무 전송 tooverify`dc.services.visualstudio.com`합니다.

## <a name="no-dependency-or-exception-data"></a>종속성 또는 예외 데이터 없음
[종속성 원격 분석](app-insights-asp-net-dependencies.md) 및 [예외 원격 분석](app-insights-asp-net-exceptions.md)을 참조하세요.

## <a name="no-performance-data"></a>성능 데이터 없음
성능 데이터(CPU, IO 속도 등)는 [Java 웹 서비스](app-insights-java-collectd.md), [Windows 데스크톱 앱](app-insights-windows-desktop.md), [IIS Web Apps 및 서비스(상태 모니터를 설치한 경우)](app-insights-monitor-performance-live-website-now.md) 및 [Azure Cloud Services](app-insights-azure.md)에 사용할 수 있습니다. 이 내용은 설정, 서버 아래에 있습니다.

Azure 웹 사이트에는 사용할 수는 없습니다.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>(서버) 데이터가 있습니까으로 게시 되었으므로 응용 프로그램 toomy 서버 hello
* 모든 Microsoft hello 실제로 복사 했는지 확인 하십시오. Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll 함께 ApplicationInsights Dll toohello 서버
* 하려면 방화벽에서 해야할 너무[일부 TCP 포트를 열어야](app-insights-ip-addresses.md#data-access-api)합니다.
* 회사 네트워크에서 프록시 toosend toouse 있으면 설정 [defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) web.config
* Windows Server 2008: hello 다음 업데이트를 설치 했는지 확인 하십시오: [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217)합니다.

## <a name="i-used-toosee-data-but-it-has-stopped"></a>중지 된 하지만 toosee 데이터 사용
* Hello 확인 [상태 블로그](http://blogs.msdn.com/b/applicationinsights-status/)합니다.
* 데이터 요소의 월간 할당량에 도달했습니까? Hello 설정/할당량 및 가격 책정 toofind 아웃를 엽니다. 그렇다면 계획을 업그레이드하거나 추가 용량에 대한 비용을 지불할 수 있습니다. Hello 참조 [가격 체계](https://azure.microsoft.com/pricing/details/application-insights/)합니다.

## <a name="i-dont-see-all-hello-data-im-expecting"></a>필요한 데 I hello 데이터를 모두 표시 되지 않습니다.
응용 프로그램에서 많은 양의 데이터가 사용 하는 경우 ASP.NET 버전 2.0.0-beta3에 대 한 Application Insights SDK hello 또는 이상 버전에서는 환영 [적응 샘플링](app-insights-sampling.md) 기능 작동 하 고 원격 분석의 일부분만 보낼 수 있습니다. 

이 기능을 비활성화할 수는 있지만 그러지 않는 것이 좋습니다. 샘플링은 진단을 목적으로 관련 원격 분석이 올바르게 전송되도록 설계되었습니다. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>사용자 원격 분석에 잘못된 지리적 데이터
IP 주소에서 파생 된 hello city, 지역 및 국가 차원에는 정확한 항상 되지 않으며.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Azure 클라우드 서비스에서 실행할 때의 "메서드를 찾을 수 없음" 예외
.NET 4.6용으로 빌드하셨나요? 4.6은 Azure 클라우드 서비스 역할에서 자동으로 지원되지 않습니다. [각 역할에 4.6을 설치](../cloud-services/cloud-services-dotnet-install-dotnet.md) 합니다.

## <a name="still-not-working"></a>여전히 작동하지 않습니다.
* [Application Insights 포럼](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

