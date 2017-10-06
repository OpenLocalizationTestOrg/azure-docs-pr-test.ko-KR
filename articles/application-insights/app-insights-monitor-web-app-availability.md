---
title: "aaaMonitor 가용성 및 응답성 모든 웹 사이트 | Microsoft Docs"
description: "Application Insights에서 웹 테스트를 설정합니다. 웹 사이트가 사용할 수 없게 되거나 느리게 응답하는 경우 알림이 제공됩니다."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>웹 사이트의 가용성 및 응답성 모니터링
웹 앱 또는 웹 사이트 tooany 서버 배포 후의 가용성 및 응답성 테스트 toomonitor를 설정할 수 있습니다. [Azure Application Insights](app-insights-overview.md) 웹 요청 tooyour 응용 프로그램 일정 한 간격에서 전송 하는 hello world 중심으로 점을 합니다. 응용 프로그램이 응답하지 않거나 느리게 응답하는 경우 사용자에게 경고할 수 있습니다.

모든 HTTP에 대 한 가용성 테스트를 설정할 수 있습니다 또는 HTTPS 끝점에서 액세스할 수 있는 공용 인터넷 hello 합니다. 없는 tooadd 어느 것에 toohello 웹 사이트를 테스트 합니다. 도 없는 toobe 사이트: 하면 종속 된 REST API 서비스를 테스트할 수 있습니다.

가용성 테스트는 다음과 같은 두 종류가 있습니다.

* [URL ping 테스트](#create): hello Azure 포털에서에서 만들 수 있는 간단 하 게 테스트 합니다.
* [Multi-step 웹 테스트](#multi-step-web-tests): Visual Studio Enterprise 및 업로드 toohello 포털에서 만들어진 합니다.

응용 프로그램 리소스 당 too25 가용성 테스트를 만들 수 있습니다.

## <a name="create"></a>1. 가용성 테스트 보고서에 대한 리소스 열기

**Application Insights를 이미 구성한 경우** 웹 앱에 대 한 hello에 Application Insights 리소스를 열고 [Azure 포털](https://portal.azure.com)합니다.

**또는 toosee 새 리소스에서 보고서를 원하는 경우** 너무 등록[Microsoft Azure](http://azure.com), toohello 이동 [Azure 포털](https://portal.azure.com), Application Insights 리소스를 만듭니다.

![새로 만들기 > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

클릭 **모든 리소스** tooopen hello 개요 블레이드에 hello 새 리소스에 대 한 합니다.

## <a name="setup"></a>2. URL ping 테스트 만들기
Hello 가용성 블레이드를 열고 테스트를 추가 합니다.

![채우기 이상 웹 사이트의 URL을 hello](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **hello URL** 모든 웹 페이지 수, tootest 싶지만에서 표시 되어야 합니다 공용 인터넷 hello 합니다. hello URL 쿼리 문자열을 포함할 수 있습니다. 따라서 데이터베이스 사용 등을 연습해 볼 수 있습니다. Hello URL tooa 리디렉션 확인 되 면 too10 리디렉션을 추가 작업 했습니다.
* **종속 요청을 구문 분석**:이 옵션을 선택 하는 경우 이미지, 스크립트, 스타일의 파일 및 기타 파일을 테스트 중인 hello 웹 페이지의 일부 hello 테스트를 요청 합니다. hello 기록 된 응답 시간 hello에 걸린 시간 tooget 이러한 파일 포함합니다. hello 테스트가 hello 전체 테스트에 대 한 hello 시간 제한 내에서 이러한 모든 리소스를 성공적으로 다운로드할 수 없는 경우 실패 합니다. 

    Hello 옵션을 선택 하지 않으면 hello 테스트 hello 파일에서 지정한 hello URL만 요청 합니다.
* **다시 시도 횟수를 사용 하도록 설정**: 짧은 간격 후에 다시 시도 됩니다 hello 테스트가 실패 하는 경우이 옵션을 선택 하면, 하는 경우. 연속 된 세 번의 시도가 실패하는 경우에 실패가 보고됩니다. 그런 다음 후속 테스트 hello 일반적인 테스트 빈도로 수행 됩니다. 다시 시도 hello 다음 성공할 때까지 일시적으로 중단 됩니다. 이 규칙은 각 테스트 위치에서 독립적으로 적용됩니다. 이 옵션을 권장합니다. 평균 실패의 약 80%는 다시 시도에서 사라집니다.
* **테스트 빈도**: 얼마나 자주 hello 테스트를 실행 각 테스트 위치에서 설정 합니다. 5분에 5번의 테스트를 하는 빈도로 사이트를 평균 1분마다 테스트합니다.
* **테스트 위치** hello 웹 요청 tooyour URL 보낼 하는 서버에서 배치 됩니다. 웹 사이트의 문제와 네트워크 문제를 구분할 수 있도록 한 가지 이상을 선택합니다. Too16 위치를 선택할 수 있습니다.
* **성공 조건**:

    **테스트 시간 제한**: 느린 응답에 대 한 경고를 발생 시킬 값 toobe이 감소 합니다. 이 기간 내 사이트의 hello 응답을 받지 못했습니다 경우 hello 테스트를 실패로 계산 됩니다. 선택한 경우 **종속 요청을 구문 분석**, 이미지, 스타일의 파일, 스크립트, 모든 hello 다음 및 다른 종속 된 리소스도이 기간 내에서 수신 합니다.

    **HTTP 응답**: hello를 성공으로 계산 하는 상태 코드를 반환 합니다. 200은 일반적인 웹 페이지 반환 되었습니다. 나타내는 hello 코드입니다.

    "Welcome!"과 같은 **콘텐츠 일치** 문자열. 정확한 대/소문자 구분 일치가 모든 응답에서 발생하는지 테스트합니다. 와일드카드 없는 일반 문자열이어야 합니다. Tooupdate 해야할 페이지 콘텐츠 변경 내용이 되는 경우 반드시 것입니다.
* **경고** 인 기본적으로 tooyou 경우 전송 오류가 발생 하는 세 위치 (5 분)입니다. 실패 한 위치에서 네트워크 문제일 가능성이 toobe 이며 사이트와 문제가 아닙니다. 하지만 더 많은 hello 임계값 toobe 변경할 수 있습니다 또는 중요 하 고 덜 수 hello 전자 메일 사용자를 변경 해야 보낼 수를 합니다.

    경고가 발생하면 호출되는 [웹후크](../monitoring-and-diagnostics/insights-webhooks-alerts.md)를 설정할 수 있습니다. 그러나 현재 쿼리 매개 변수는 속성으로 전달되지 않습니다.

### <a name="test-more-urls"></a>더 많은 URL 테스트
테스트를 더 추가 합니다. 예를 들어 더하기 tootesting 홈 페이지에 있습니다 되었는지 확인할 수 검색에 대 한 hello URL을 테스트 하 여 데이터베이스를 실행 합니다.


## <a name="monitor"></a>3. 가용성 테스트 결과 참조

몇 분 후 클릭 **새로 고침** toosee 테스트 결과입니다. 

![Hello 홈 블레이드의 요약 결과](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

hello scatterplot hello의 샘플 진단 테스트 단계 세부 개 테스트 결과 보여 줍니다. hello 테스트 엔진 오류가 발생 한 테스트에 대 한 진단 정보를 저장 합니다. 성공적인 테스트에 대 한 hello 실행의 하위 집합에 대 한 진단 세부 정보가 저장 됩니다. Hello 녹색/빨간색 점 toosee hello 테스트 타임 스탬프, 테스트 지속 시간, 위치 및 테스트 이름 위로 가져갑니다. Hello 산 점도 toosee hello 결과의 세부 정보 hello 테스트에서에서 모든 점을 클릭 합니다.  

특정 테스트, 위치를 선택 하거나 hello 시간 기간 toosee 더 결과 hello 주위 관심 있는 기간을 단축 합니다. 탐색기 검색 toosee 결과 모든 실행에서 사용 하거나이 데이터에 분석 쿼리 toorun 사용자 지정 보고서를 사용 합니다.

또한 toohello 원시 결과에 두 가지 가용성 메트릭이 있습니다 메트릭 탐색기에서: 

1. 모든 테스트 실행에서 성공 했 hello 테스트의 사용 가능성: 비율입니다. 
2. 테스트 지속 시간: 모든 테스트 실행에서의 평균 테스트 지속 시간입니다.

Hello 테스트 이름, 위치 tooanalyze 추세는 특정 테스트 및/또는 위치에 필터를 적용할 수 있습니다.

## <a name="edit"></a>테스트 검사 및 편집

Hello 요약 페이지에서 특정 테스트를 선택 합니다. 거기에서 해당 특정 결과를 확인하고 편집하거나 일시적으로 사용하지 않도록 설정할 수 있습니다.

![웹 테스트 편집 또는 사용 안 함](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

서비스에서 유지 관리를 수행 하는 동안 규칙 관련 된 hello 경고 또는 toodisable 가용성 테스트를 할 수 있습니다. 

## <a name="failures"></a>오류가 표시되는 경우
빨간 점을 클릭합니다.

![빨간 점을 클릭 합니다.](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


가용성 테스트 결과에서 다음을 수행할 수 있습니다.

* 서버에서 받은 hello 응답을 검사 합니다.
* Hello 실패 한 요청 인스턴스를 처리 하는 동안 서버 응용 프로그램에서 보낸 hello 원격 분석을 엽니다.
* Git 또는 VSTS tootrack hello 문제에서 작업 항목 하거나 문제를 기록 합니다. hello 버그 링크 toothis 이벤트를 포함 됩니다.
* Visual Studio에서 hello 웹 테스트 결과를 엽니다.


*정상으로 보이지만 실패로 보고되었습니까?* 모든 hello 이미지, 스크립트, 스타일 시트 및 hello 페이지에 의해 로드 하는 다른 모든 파일을 확인 합니다. 그 중 하나라도 실패 하면 hello 테스트 보고 되며 실패 한 hello 기본 html 페이지 확인을 로드 하는 경우.

*관련 항목이 없나요?* 서버 쪽 응용 프로그램에 대해 Application Insights를 설정한 경우, [샘플링](app-insights-sampling.md)이 작동 중이기 때문일 수 있습니다. 

## <a name="multi-step-web-tests"></a>다중 단계 웹 테스트
URL 시퀀스를 포함하는 시나리오를 모니터링할 수 있습니다. 예를 들어 판매 웹 사이트를 모니터링 하는 경우 추가 항목 toohello 쇼핑 카트 제대로 작동 하는지 테스트할 수 있습니다.

> [!NOTE] 
> 다단계 웹 테스트에 대한 요금이 청구됩니다. [가격 체계](http://azure.microsoft.com/pricing/details/application-insights/).
> 

toocreate multi-step 테스트를 Visual Studio Enterprise를 사용 하 여 hello 시나리오 기록 한 다음 업로드할 있습니다 hello tooApplication 통찰력을 기록 합니다. Application Insights 간격 hello 시나리오를 재생 하 고 hello 응답을 확인 합니다.

> [!NOTE]
> 테스트에서 코딩된 함수 또는 루프를 사용할 수 없습니다. hello 테스트 hello.webtest 스크립트에 완전히 포함 되어야 합니다. 그러나 표준 플러그 인을 사용할 수 있습니다.
>

#### <a name="1-record-a-scenario"></a>1. 시나리오 기록
Visual Studio Enterprise를 사용 하 여 웹 세션 toorecord 합니다.

1. 웹 성능 테스트 프로젝트를 만듭니다.

    ![Visual Studio Enterprise edition에서 hello 웹 성능 및 부하 테스트 템플릿에서 프로젝트를 만듭니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *Hello 웹 성능 및 부하 테스트 템플릿이 보이지 않으세요?* - Visual Studio Enterprise를 닫습니다. 열기 **Visual Studio 설치 관리자** toomodify Visual Studio Enterprise 설치 합니다. **개별 구성 요소** 아래에서 **웹 성능 및 부하 테스트 도구**를 선택합니다.

2. Hello.webtest 파일을 열고 기록을 시작 합니다.

    ![Hello.webtest 파일을 열고 레코드를 클릭 합니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. 사용자 작업 toosimulate 테스트에서 원하는 hello지 않습니다: 웹 사이트를 열고, 추가 제품 toohello 카트 등입니다. 테스트를 중지합니다.

    ![hello 웹 테스트 레코더 실행 Internet Explorer에서 사용 합니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    시나리오를 길게 만들지 마세요. 100개 단계와 2 분으로 제한됩니다.
4. Hello 테스트를 편집 합니다.

   * 유효성 검사 toocheck 받은 hello 텍스트 및 응답 코드를 추가 합니다.
   * 불필요한 상호 작용을 모두 제거합니다. 또한 그림 또는 tooad 또는 사이트를 추적에 대 한 종속 요청을 제거할 수 있습니다.

     Hello 테스트 스크립트 편집할 수 있습니다-사용자 지정 코드를 추가 하거나 다른 웹 테스트를 호출 해야 합니다. Hello 테스트에 루프를 삽입 하지 마십시오. 표준 웹 테스트 플러그 인을 사용할 수 있습니다.
5. Visual Studio toomake 작동의 hello 테스트를 실행 합니다.

    hello 웹 테스트 러너 웹 브라우저를 열고 반복 hello 기록한 작업. 예상대로 작동하는지 확인합니다.

    ![Visual Studio에서 hello.webtest 파일을 열고 실행을 클릭 합니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2. Hello 웹 테스트 tooApplication Insights 업로드
1. Hello Application Insights 포털에서 웹 테스트를 만듭니다.

    ![Hello 웹 테스트 블레이드에서 추가 선택 합니다.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. 여러 단계의 테스트를 선택 하 고 hello.webtest 파일을 업로드 합니다.

    ![다단계 웹 테스트를 선택합니다.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Hello 테스트 위치 설정, 빈도 및 경고 매개 변수 hello에 ping 용 방식으로 동일한 테스트 합니다.

#### <a name="3-see-hello-results"></a>3. Hello 결과 참조 하십시오.

보고 테스트 결과 및 오류 hello 동일한 방식으로 단일 url 테스트 합니다.

테스트 결과 tooview hello를 다운로드할 수는 또한 Visual Studio에서 해당 합니다.

#### <a name="too-many-failures"></a>오류가 너무 많나요?

* 실패에 대 한 일반적인 이유는 해당 hello 테스트 너무 오래 실행 될 합니다. 2분 이내로 실행해야 합니다.

* 반드시 hello 테스트 toosucceed, 스크립트, 스타일 시트, 이미지 등을 포함 하 여에 대 한 페이지의 모든 hello 리소스 올바르게 로드 해야 합니다.

* hello 웹 테스트 완전히에 포함 되어야 합니다 hello.webtest 스크립트: hello 테스트에 코딩 된 함수를 사용할 수 없습니다.

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>다단계 테스트에 시간 및 난수 연결
외부 피드에서 주식과 같이 시간에 따라 변하는 데이터를 가져오는 도구를 테스트한다고 가정합니다. 웹 테스트를 기록할 때 toouse 특정 시간 있지만 StartTime과 EndTime의 hello 매개 변수 테스트 설정.

![매개 변수를 가진 웹 테스트입니다.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

EndTime toobe hello 시간을 표시 하는 항상 원하는 StartTime 15 분 이어야 합니다 hello 테스트를 실행할 때 이전에 수행 합니다.

웹 테스트 플러그 인에 toodo 시간 매개 변수화 하는 hello 방법을 제공 합니다.

1. 원하는 각 가변 매개 변수 값에 대한 웹 테스트 플러그 인을 추가합니다. Hello 웹 테스트 도구 모음에서 선택 **웹 테스트 플러그 인 추가**합니다.

    ![웹 테스트 플러그인 추가를 선택하고 형식을 선택합니다.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    이 예에서는 날짜 시간 Plug-in hello의 두 인스턴스가 사용 합니다. 한 인스턴스는 "15분 전"이고 다른 하나는 "지금"입니다.
2. 각 플러그 인의 hello 속성을 엽니다. 이름을 지정 하 고 현재 시간 toouse hello 설정 합니다. 둘 중 하나에 대해 Add Minutes = -15를 설정합니다.

    ![이름을 설정하고, 현재 시간을 사용하며 시간을 추가합니다.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. Hello 웹 테스트 매개 변수에서 {{name} 플러그 인} tooreference 플러그 인 이름을 사용 합니다.

    ![Hello 테스트 매개 변수, {{name} 플러그 인을 (를) 사용 합니다.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

이제 테스트 toohello 포털을 업로드 합니다. Hello 테스트의 모든 실행에서 동적 값 hello를 사용합니다.

## <a name="dealing-with-sign-in"></a>로그인 처리
사용자가 tooyour 앱에 로그인 하는 경우 뒤에 hello 로그인 페이지를 테스트할 수 있도록 로그인 시뮬레이션 하는 데는 다양 한 옵션이 있습니다. 사용 하는 hello 방법 hello 유형의 hello 응용 프로그램에서 제공 하는 보안에 따라 다릅니다.

모든 경우에만 테스트 목적 hello에 대 한 응용 프로그램에서 계정을 만들어야 합니다. 가능 하면 두는 실제 사용자에 게 영향을 주는 hello 웹 테스트 가능성이 hello 계정의 권한으로이 테스트를 제한 합니다.

### <a name="simple-username-and-password"></a>간단한 사용자 이름 및 암호
Hello에서 웹 테스트를 기록 일반적인 방법입니다. 우선 쿠키를 삭제합니다.

### <a name="saml-authentication"></a>SAML 인정
웹 테스트에 사용할 수 있는 hello SAML 플러그 인을 사용 합니다.

### <a name="client-secret"></a>클라이언트 암호
앱에 클라이언트 암호를 포함하는 로그인 경로가 있는 경우 해당 경로를 사용합니다. AAD(Azure Active Directory)는 클라이언트 암호 로그인을 제공하는 서비스의 예입니다. AAD에서 hello 클라이언트 암호는 hello 앱 키입니다.

앱 키를 사용하는 Azure 웹앱의 샘플 웹 테스트는 다음과 같습니다.

![클라이언트 암호 샘플](./media/app-insights-monitor-web-app-availability/110.png)

1. 클라이언트 암호(AppKey)를 사용하여 AAD에서 토큰을 가져옵니다.
2. 응답에서 전달자 토큰을 추출합니다.
3. 전달자 토큰을 사용 하 여 hello 인증 헤더에 API를 호출 합니다.

Hello 웹 테스트는 실제 클라이언트--AAD에서 자체 응용 프로그램 즉,에 있는지 확인 하 고 해당 clientId + appkey를 사용 합니다. 테스트 대상 서비스에서 AAD 자체 응용 프로그램을 갖도록: hello appID이 응용이 프로그램의 URI는 hello "resource" 필드에 hello 웹 테스트에 반영 됩니다.

### <a name="open-authentication"></a>공개 인증
공개 인증의 예는 Microsoft 또는 Google 계정으로 로그인하는 것입니다. 많은 응용 프로그램을 사용 하 여 OAuth 제공 hello 클라이언트 비밀 대신에 첫 번째 방법은 tooinvestigate 이어야 합니다.이 가능성입니다.

테스트 해야 OAuth를 사용 하 여 로그인 하는 경우 hello 일반적인 방법이입니다.

* Fiddler tooexamine hello 트래픽 앱, 웹 브라우저 및 hello 인증 사이트와 같은 도구를 사용 합니다.
* 두 개 이상의 로그인 서로 다른 컴퓨터 또는 브라우저를 사용 하 여 수행 하거나 (tooallow 토큰 tooexpire) 긴 간격입니다.
* 서로 다른 세션을 비교 하 여 로그인 한 후 응용 프로그램 서버 tooyour 전달 되는 사이트를 인증 하는 hello에서 다시 전달 하는 hello 토큰을 식별 합니다.
* Visual Studio Online을 사용하여 웹 테스트 기록
* Hello 토큰 hello 인증자에서 반환 되 면 hello 매개 변수를 설정 하 고 hello 쿼리 toohello 사이트에서 사용 하 여 hello 토큰 매개 변수화 합니다.
  (Visual Studio tooparameterize hello 테스트 하려고 하지만 hello 토큰 올바르게 매개 변수화 되지 않습니다.)


## <a name="performance-tests"></a>성능 테스트
웹 사이트에 부하 테스트를 실행할 수 있습니다. Hello 가용성 테스트와 같은 hello 전 세계이 지점에서 간단한 요청 또는 multi-step 요청을 보낼 수 있습니다. 가용성 테스트와는 달리 많은 요청이 전송되어 여러 동시 사용자를 시뮬레이션합니다.

Hello 개요 블레이드에서 엽니다 **설정**, **성능 테스트**합니다. 초대는 테스트를 만들 때 tooconnect tooor Visual Studio Team Services 계정을 만듭니다.

Hello 테스트 완료 되 면 응답 시간과 성공률 표시 됩니다.


![성능 테스트](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> 성능 테스트의 tooobserve hello 효과 사용 하 여 [라이브 스트림을](app-insights-live-stream.md) 및 [프로파일러](app-insights-profiler.md)합니다.
>

## <a name="automation"></a>Automation
* [PowerShell 스크립트 tooset 가용성 테스트를 사용 하 여](app-insights-powershell.md#add-an-availability-test) 자동으로 합니다.
* 경고가 발생하면 호출되는 [웹후크](../monitoring-and-diagnostics/insights-webhooks-alerts.md)를 설정합니다.

## <a name="qna"></a>질문이 있습니까? 문제가 있습니까?
* *웹 테스트에서 코드를 호출할 수 있나요?*

    아니요. hello hello 테스트 단계 hello.webtest 파일에 있어야 합니다. 또한 다른 웹 테스트를 호출하거나 루프를 사용할 수 없습니다. 그러나 몇 가지 유용한 플러그 인이 있습니다.
* *HTTPS가 지원됩니까?*

    TLS 1.1 및 TLS 1.2를 지원합니다.
* *"웹 테스트" 및 "가용성 테스트" 간의 차이가 있나요?*

    hello 두 용어 참조 될 수 있습니다 같은 의미로 합니다. 가용성 테스트 hello 단일 URL ping을 포함 하는 보다 일반적인 용어 테스트 또한 toohello multi-step 웹 테스트입니다.
* *방화벽 뒤에서 실행 되는 내부 서버에서 toouse 가용성 테스트를 하겠습니다.*

    가능한 해결 방법으로 다음 두 가지가 있습니다.
    
    * 방화벽 toopermit 들어오는 요청에서 hello 구성 [웹의 IP 주소 테스트 에이전트](app-insights-ip-addresses.md)합니다.
    * 내부 서버 tooperiodically 테스트 사용자 고유의 코드를 작성 합니다. 방화벽 뒤에 있는 테스트 서버에서 백그라운드 프로세스로 hello 코드를 실행 합니다. 테스트 프로세스 결과 보낼 수는 tooApplication Insights를 사용 하 여 [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) hello 핵심 SDK 패키지에서 API입니다. 이 위해서는 테스트 서버 toohave 나가는 액세스 toohello Application Insights 수집 끝점에 있지만 hello의 들어오는 요청을 허용 하는 대체 항목 보다 훨씬 더 작은 보안 위험. hello 결과가 hello 가용성 웹 테스트 블레이드에 표시 되지 않습니다 되지만 분석, 검색 및 메트릭 탐색기에서 가용성 결과으로 나타납니다.
* *다중 단계 웹 테스트 업로드 실패*

    300K의 크기 제한이 있습니다.

    루프는 지원되지 않습니다.

    참조 tooother 웹 테스트가 지원 되지 않습니다.

    데이터 원본은 지원되지 않습니다.
* *다중 단계 테스트가 완료되지 않습니다.*

    테스트당 100개 요청의 제한이 있습니다.

    hello 테스트 2 분 이상 실행 하는 경우 중지 됩니다.
* *클라이언트 인증서로 테스트를 실행하는 방법*

    죄송합니다만, 지원되지 않습니다.


## <a name="next"></a>다음 단계
[진단 로그 검색][diagnostic]

[문제 해결][qna]

[웹 테스트 에이전트의 IP 주소](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
