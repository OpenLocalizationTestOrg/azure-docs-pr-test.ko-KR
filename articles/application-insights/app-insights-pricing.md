---
title: "Azure Application Insights에 대 한 가격 및 데이터 볼륨 aaaManage | Microsoft Docs"
description: "Application Insights에서 원격 분석을 관리하고 비용을 모니터링합니다."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>Application Insights에서 가격 및 데이터 볼륨 관리


[Azure Application Insights][start]의 가격 책정은 응용 프로그램당 데이터 볼륨을 기반으로 합니다. 낮은 개발 중 이나는 작은 응용 프로그램에 대 한 사용량이 가능성이 toobe 가능한 원격 분석 데이터의 1GB 월별 여유 있기 때문에 있습니다.

각 Application Insights 리소스를 별도 서비스로 요금이 부과 됩니다 및 toohello 청구서 구독 tooAzure에 대 한 영향을 줍니다.

가격 책정 계획에는 두 가지가 있습니다. 기본 계획 hello Basic를 라고 합니다. 일별 요금은 갖지만 같은 특정 추가 기능을 사용할 수 있는 hello 엔터프라이즈 계획을 선택 하면 [연속 내보내기를](app-insights-export-telemetry.md)합니다.

Application Insights에 대 한 가격 책정 작동 방식에 대 한 질문이 있으면 생각 될 무료 toopost에 질문 우리의 [포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights)합니다. 

## <a name="hello-price-plans"></a>hello 가격 계획

Hello 참조 [Application Insights 가격 책정 페이지] [ pricing] 통화에서 현재 가격에 대 한 합니다.

### <a name="basic-plan"></a>기본 계획

기본 계획 hello hello 기본 있으면 새 Application Insights 리소스를 만들고 대부분의 고객에 대 한 충분 합니다.

* Hello 기본 계획에서 데이터 볼륨으로 청구 됩니다:의 Application Insights에서 수신 하는 원격 분석의 바이트 수입니다. Application Insights 응용 프로그램에서 받은 압축 되지 않은 hello JSON 데이터 패키지의 hello 크기와 같은 데이터 볼륨 측정 됩니다.
에 대 한 [분석으로 가져온 테이블 형식 데이터](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import), 보낸 파일 tooApplication Insights의 압축 되지 않은 크기를 hello 대로 hello 데이터 볼륨 측정 됩니다.  
* 각 앱에 대 한 첫 번째 사용자 1GB, 무료 이므로 나 가능성이 toohave toopay 하는 방금 실험 또는 개발 하는 경우.
* [라이브 메트릭 스트림](app-insights-live-stream.md) 데이터는 가격 책정에 계산 되지 않습니다.
* [연속 내보내기를](app-insights-export-telemetry.md) hello 기본 계획의 경우 GB 당 추가 요금에 사용할 수 있는입니다.

### <a name="enterprise-plan"></a>엔터프라이즈 계획

* Hello Enterprise 계획에 앱 Application Insights의 모든 hello 기능을 사용할 수 있습니다. [연속 내보내기](app-insights-export-telemetry.md) 및 

[로그 분석 커넥터](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409) hello 엔터프라이즈 계획을 추가 요금 없이 사용할 수 있습니다.
* 모든 앱에 대 한 원격 분석 hello Enterprise 계획에 보내는 노드당 지불 합니다. 
 * *노드*는 앱을 호스팅하는 실제/가상 서버 컴퓨터 또는 PaaS(Platform-as-a-Service) 역할 인스턴스입니다.
 * 개발 컴퓨터, 클라이언트 브라우저 및 모바일 장치는 노드로 계산되지 않습니다.
 * 원격 분석을 보내는 여러 구성 요소(예: 웹 서비스 및 백 엔드 작업자)가 앱에 있는 경우 개별적으로 집계됩니다.
 * [라이브 메트릭 스트림](app-insights-live-stream.md) 데이터는 가격 책정에 계산되지 않습니다.* 요금은 구독을 통해 앱 기준이 아니라 노드 기준으로 부과됩니다. 5 개의 노드가 12 앱의 경우 다음 hello는 5 개의 노드에 대 한 청구에 대 한 원격 분석을 보내는 경우에 합니다.
* 요금이 매월 견적되지만 노드에서 앱의 원격 분석을 보내는 모든 시간에 대해서만 부과됩니다. hello 시간당 요금은 hello quoted 월별 요금 / 744 (31 일 기간의 시간 hello).
* 시간별로 감지되는 각 노드에 대해 1일 200MB의 데이터 볼륨 할당이 제공됩니다. 사용 하지 않는 데이터 할당 지연 되지 않습니다 toohello 1 일에서에서 다음 합니다.
 * Hello 엔터프라이즈 가격 책정 옵션을 선택 하면 각 구독 hello 해당 구독에서 원격 분석 toohello Application Insights 리소스를 전송 하는 노드 수에 따라 데이터의 일일 허용 한 도를 가져옵니다. 하루 종일 데이터를 전송 하는 5 개의 노드가 있는 경우 해당 구독에 적용 1GB tooall hello Application Insights 리소스 풀링된 허용 해야 합니다. 특정 노드가 모든 노드에서 공유 hello 데이터를 포함 하기 때문에 다른 노드 보다 더 많은 데이터를 보낼 경우 문제가 되지 않습니다. 지정된 된 날에 hello Application Insights 리소스 hello이이 구독에 대 한 일별 데이터 할당에 포함 된 보다 많은 데이터를 받을 경우 hello GB 당 초과 데이터 요금이 부과 됩니다. 
 * hello 일일 데이터 허용 한도 hello hello 일 (UTC를 사용 하 여)의 시간으로 계산 됩니다 각 노드에 원격 분석 24 시간 200MB로 나눈 값을 보내는 지 합니다. Hello 그 날 것에 대 한 데이터를 포함 hello 하루에서 24 시간 동안 15의 hello 시 원격 분석을 보내는 4 개의 노드가 있는 경우 ((4 x 15) / 24) x 200 MB = 500 MB입니다. 2.30 usd GB 당 가격 데이터 초과 대 한 hello, hello 청구에 대 한 hello 노드 그 날 1GB의 데이터를 보낼 경우 1.15 USD 됩니다.
 * Hello 엔터프라이즈 계획의 일일 허용 한도를 hello 기본 옵션을 선택한 응용 프로그램와 공유 되지 않습니다 기록한 사용 하지 않는 여유 일상적인 지연 되지 않습니다. 
* 식별되는 노드 수를 결정하는 몇 가지 예는 다음과 같습니다.
| 시나리오                               | 일일 총 노드 수 |
|:---------------------------------------|:----------------:|
| 1개 응용 프로그램에서 3개 Azure App Service 인스턴스 및 1개 가상 서버를 사용합니다. | 4 |
| 이러한 응용 프로그램은 동일한 구독 hello 및 hello Enterprise 계획에 대 한 2 개의 Vm, 및 hello Application Insights 리소스에서 실행 되는 3 응용 프로그램 | 2 | 
| 4 응용 프로그램에는 해당 응용 프로그램 Insights 리소스가 hello 동일한 구독 합니다. 각 응용 프로그램마다 16 비최대 사용 시간 동안 2개 인스턴스를 실행하고, 8 최대 사용 시간 동안 4개 인스턴스를 실행합니다. | 13.33 | 
| 1개 작업자 역할 및 1개 웹 역할이 부여된 클라우드 서비스에서 각 역할마다 2개 인스턴스를 실행합니다. | 4 | 
| 50개 마이크로 서비스를 실행하는 5개 노드 Service Fabric 클러스터에서 각 마이크로 서비스마다 3개 인스턴스를 실행합니다. | 5|

* hello 정확한 노드 수를 세 동작에 따라 Application Insights SDK 응용 프로그램은 사용 하 여 다릅니다. 
  * SDK 버전 2.2에서에서 Application Insights 둘 다 hello 부터는 및 [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) 또는 [웹 SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) 노드로 각 응용 프로그램 호스트를 보고, 예를 들어 물리적 서버 및 VM 호스트 또는 hello에 대 한 컴퓨터 이름을 hello 됩니다 클라우드 서비스의 hello 경우에서 인스턴스 이름입니다.  만 사용 하 여 예외는 응용 프로그램에만 hello [.NET Core](https://dotnet.github.io/) 및 hello는 하나의 노드만 사례 보고 됩니다 모든 호스트에 대 한 hello 호스트 이름을 사용할 수 없기 때문에 Application Insights Core SDK입니다. 
  * 그러나 Hello SDK의 이전 버전에 대 한 hello [웹 SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) hello 최신 SDK 버전에서 hello와 마찬가지로 동작 [Core SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) 실제 응용 프로그램 호스트의 hello 수에 관계 없이 하나의 노드를 보고 합니다. 
  * 응용 프로그램 hello SDK tooset roleInstance tooa 사용자 지정 값을 사용 하는 경우 기본적으로 동일 하 게 값 됩니다 toodetermine hello 노드 수를 사용 합니다. 
  * 새 SDK 버전 클라이언트 컴퓨터 또는 모바일 장치에서 실행 되는 앱을 사용 하는 경우 있기 hello 노드 수 (hello 많은 수의 클라이언트 컴퓨터 또는 모바일 장치)에서 매우 큰 숫자가 반환할 수 있습니다. 

### <a name="multi-step-web-tests"></a>다중 단계 웹 테스트

[다중 단계 웹 테스트](app-insights-monitor-web-app-availability.md#multi-step-web-tests)에 대한 추가 요금이 있습니다. 이 일련의 동작을 수행 하는 tooweb 테스트를 나타냅니다. 

단일 페이지의 'ping 테스트'에 대해 별도의 요금이 부과되지 않습니다. ping 테스트와 다중 단계 테스트 모두의 원격 분석은 앱의 다른 원격 분석과 함께 청구됩니다.
 
## <a name="operations-management-suite-subscription-entitlement"></a>Operations Management Suite 구독 자격

으로 [최근에 발표](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/), Microsoft Operations Management Suite E1 및 e 2를 구입한 고객에 게 추가 비용 없이 추가 구성 요소로 수 tooget Insights 엔터프라이즈 응용 프로그램을 됩니다. 특히 각 단위 Operations Management Suite E1 및 e 2에 Application Insights의 hello 엔터프라이즈 계획의 권한 too1 노드는 포함 되어 있습니다. 위에서 언급 한 대로 Application Insights 노드마다 too200 m B의 추가 비용 없이 90 일 간의 데이터 보존 (별도의 로그 분석 데이터 수집), 하루 수집 된 데이터를 포함 합니다. 

> [!NOTE]
> 이 권한을 얻게 tooensure, 있어야 hello 엔터프라이즈에서 Application Insights 리소스 계획 가격 책정 합니다. 이 자격 hello 기본 계획의 Application Insights 리소스는 이점이 없습니다 하므로 노드로 적용 됩니다. 이 자격 hello에 볼 수 없게 됩니다 참고 예상 비용 hello 기능 + 가격 책정 블레이드에 표시 합니다. 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>가격 계획 검토 및 비용 추정

Applicaition Insights 가격 책정 모델을 사용할 수 있는 쉬운 toounderstand hello 및 비용 가능성이 어떤 hello를 기반 하 여 최근 사용 패턴으로 수 있습니다. 열어 hello 하 여 시작 **기능 + 가격 책정** hello hello Azure 포털에서에서 Application Insights 리소스 블레이드:

![가격 책정을 선택합니다.](./media/app-insights-pricing/01-pricing.png)

**a.** Hello 월에 대 한 데이터 볼륨을 검토 합니다. 여기에 수신 하 고 유지 모든 hello 데이터 (후 [샘플링](app-insights-sampling.md) 가용성 테스트와 서버 및 클라이언트 앱에서.

**b.** [다단계 웹 테스트](app-insights-monitor-web-app-availability.md#multi-step-web-tests)에 대해서는 별도 요금이 부과됩니다. (Hello 데이터 볼륨 충전에 포함 된 간단한 가용성 테스트를 포함 하지 않습니다.)

**c.** Enterprise 계획 hello를 사용 하도록 설정 합니다.

**d.** Hello 지난 달에 대 한 toodata 관리 옵션 tooview 데이터 볼륨을 통해 클릭 하 고 일일 한도가 설정 하거나 수집 샘플링을 설정 합니다.

응용 프로그램 통찰력 요금 tooyour Azure 청구서에 추가 됩니다. Hello 또는 hello Azure 포털의 요금 청구 섹션 hello에 요금을 청구할 Azure의 세부 정보를 볼 수 있습니다 [Azure Billing Portal](https://account.windowsazure.com/Subscriptions)합니다. 

![Hello 측면 메뉴 청구를 선택 합니다.](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>데이터 속도
세 가지 방법으로 데이터를 전송 하는 볼륨에는 hello 제한 됩니다.

* **샘플링:** 이 메커니즘을 사용할 수 있습니다 메트릭 최소 왜곡을 사용 하 여 프로그램 서버 및 클라이언트 앱에서 보내는 원격 분석의 hello 양을 줄일 수 있습니다. Hello tootune hello 양의 데이터는 기본 도구입니다. [샘플링 기능](app-insights-sampling.md)에 대해 자세히 알아보세요. 
* **일일 한도가:** 이 hello Azure 포털에서에서 Application Insights 리소스 만들기가 설정 된 경우 too500 g B/일입니다. Visual Studio에서 Application Insights 리소스를 만들 때 기본 hello은 작은 (유일한 32.3 m B/일)은 유일한 toofaciliate 테스트 위한 것입니다. 이 경우 것은 해당 hello 사용자 hello 응용 프로그램을 프로덕션 환경에 배포 하기 전에 hello 일일 한도가 발생 합니다. hello 최대 한도가 500GB/일 않는 높으며 트래픽이 많은 응용 프로그램에 대 한 높은 최대 요청 했습니다. 주의 hello 일일 한도가 설정 하는 경우 원래의 도와 속도가 **되지 toohit hello 일일 한도가**그러면 hello 일의 나머지 부분에서는 hello에 대 한 데이터가 손실 고 수 없습니다 toomonitor 응용 프로그램 때문에 있습니다. toochange 것을 사용 하 여 hello 매일 볼륨 cap 블레이드에서 hello 데이터 볼륨 관리 블레이드 (아래 참조)에서 링크. 일부 구독 유형에는 Application Insights에 사용할 수 없는 크레딧이 있으니 유의하세요. Hello 구독에 지출 한 제한, 매일 hello cap 블레이드 경우에 지침 어떻게 tooremove 하기를 사용 하도록 설정한 hello 매일 cap toobe 32.3 m B/일 이상 발생 합니다.  
* **스로틀:** 이 제한을 hello 데이터 속도 too32 k 이벤트 초당 평균 1 분 이상. 


*내 앱 속도 제한 하는 hello를 초과 하는 경우 어떻게 되나요?*

* 응용 프로그램에서 전송 하는 데이터 양이 hello 1 분 마다 평가 됩니다. Hello 초당 hello 분 당 평균을 초과할 경우 hello 서버 일부 요청을 거부 합니다. hello SDK hello 데이터를 버퍼링 한 다음 몇 분 동안 급격 한 증가 냅니다 tooresend를 시도 합니다. 앱 속도 제한 하는 hello 위에 데이터에 일관 되 게 보내면 일부 데이터가 삭제 됩니다. (hello ASP.NET, Java 및 JavaScript Sdk 시도 tooresend 이러한 방식으로, 다른 Sdk 단순히 drop 제한 된 데이터를 수 있습니다.) 제한이 발생하는 경우 이를 경고하는 알림이 표시됩니다.

*앱에서 보내는 데이터의 양을 어떻게 알 수 있습니까?*

* 열기 hello **데이터 볼륨 관리** 블레이드 toosee hello 일별 데이터 볼륨 차트입니다. 
* 또는 메트릭 탐색기에서 새 차트를 추가하고 **데이터 요소 볼륨**을 메트릭으로 선택합니다. 그룹화로 전환한 다음 **데이터 형식**을 기준으로 그룹화합니다.

## <a name="tooreduce-your-data-rate"></a>tooreduce 데이터 속도
몇 가지 사항은 tooreduce 데이터 볼륨을 수행할 수 있습니다.

* [샘플링](app-insights-sampling.md)을 사용합니다. 이 기술은 메트릭, 기울이기 및 검색에 관련된 항목 간의 hello 기능 toonavigate 중단 없이 데이터 속도를 낮춥니다. 서버 앱에서는 이 기능이 자동으로 수행됩니다.
* [Hello 보고 될 수 있는 Ajax 호출 수가 제한](app-insights-javascript.md#detailed-configuration) 모든 페이지 보기 또는 스위치를 off Ajax 보고 합니다.
* [ApplicationInsights.config를 편집](app-insights-configuration-with-applicationinsights-config.md)하여 필요하지 않은 컬렉션 모듈을 끕니다. 예를 들어 성능 카운터 또는 종속성 데이터가 필요하지 않다고 결정할 수 있습니다.
* 원격 분석 tooseparate 계측 키를 분할 합니다. 
* 메트릭을 미리 집계합니다. 응용 프로그램에서 호출 tooTrackMetric를 배치한 경우에 hello 평균을 계산 하 고 측정 한 값의 일괄 처리의 표준 편차를 허용 하는 hello 오버 로드를 사용 하 여 트래픽을 줄일 수 있습니다. 또는 [사전 집계 패키지](https://www.myget.org/gallery/applicationinsights-sdk-labs)를 사용할 수 있습니다.

## <a name="managing-hello-maximum-daily-data-volume"></a>Hello 최대 매일 데이터 볼륨 관리

Hello 매일 볼륨 cap toolimit hello 수집 된 데이터를 사용할 수 있습니다 이지만 hello 하루의 hello 나머지 부분에 대 한 응용 프로그램에서 보낸 모든 telemetery 손실 발생 됩니다 hello cap 충족 될 경우. **권장 되지는 않음** toohave 프로그램 응용 프로그램 toohit hello 일일 한도가 이후에 없습니다 tootrack hello 상태와 응용 프로그램의 성능을 적중 될 후 합니다. 

대신를 사용 하 여 [샘플링](app-insights-sampling.md) tootune hello 데이터 볼륨 toohello 수준을 하는 응용 프로그램을 예기치 않게 높은 많은 양의 telemetery 보내기 시작 하는 경우 "최후의 수단" 으로만 일일 한도가 hello를 사용 합니다. 

hello와 응용 프로그램 Insihgts 리소스의 구성 섹션에서에서 toochange hello 일일 한도가, 클릭 **데이터 볼륨 관리** 다음 **일일 한도가**합니다.

![Hello 일일 원격 분석 볼륨 한도가 조정](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>샘플링
[샘플링](app-insights-sampling.md) 는 hello 전송 속도 원격 분석은 tooyour 응용 프로그램 진단 검색 하는 동안 관련 이벤트 hello 기능 toofind 그대로 유지 하는 동안를 줄이는 방법 이며 유지 올바른 이벤트 수를 계산 합니다. 

샘플링은 tooreduce 요금이 및 월별 할당량 내에 유지 하는 효과적인 방법입니다. hello 샘플링 알고리즘 유지 원격 분석의 관련된 항목, 예를 들어 검색을 사용 하면 찾을 수 있도록 hello 요청과 관련 tooa 특정 예외입니다. 또한 hello 알고리즘 요청 속도, 예외 속도 및 기타 개수에 대 한 메트릭 탐색기에서 hello 올바른 값을 볼 수 있도록 정확한 개수를 유지 합니다.

샘플링에는 여러 가지 유형이 있습니다.

* [적응 샘플링](app-insights-sampling.md) hello 응용 프로그램에서 전송 하는 원격 분석의 toohello 볼륨을 자동으로 조정 하는 ASP.NET SDK에 대 한 hello 기본값입니다. 자동으로에서 작동 hello SDK 웹 앱의 hello 네트워크의 원격 분석 트래픽 hello를 줄일 합니다. 
* *수집 샘플링* hello 지점 응용 프로그램에서 원격 분석이 hello Application Insights 서비스에서 작동 하는 대신 사용할 수 있습니다. 응용 프로그램에서 보낸 원격 분석의 hello 볼륨 영향을 주지 않습니다 되지만 hello 서비스에 의해 보존 된 hello 볼륨은 줄어듭니다. Tooreduce hello 할당량에서 브라우저와 다른 Sdk 원격 분석 사용 하는 사용할 수 있습니다.

샘플링의 경우 tooset 수집 hello 가격 책정 블레이드에서 hello 제어를 설정 합니다.

![Hello 할당량 및 가격 블레이드 hello 예제 부분을 클릭 하 고 샘플링 비율을 선택 합니다.](./media/app-insights-pricing/04.png)

> [!WARNING]
> hello 데이터 샘플링 블레이드 수집 샘플링의 hello 값을 제어합니다. 응용 프로그램에 Application Insights SDK hello에서 적용 되는 hello 샘플링 속도 반영 되지 않습니다. Hello SDK에 들어오는 원격 분석 hello를 이미 샘플링 수집 샘플링 적용 되지 않습니다.
> 

실제 toodiscover hello 샘플링 속도 적용 한에 관계 없이 사용 하 여 프로그램 [분석 쿼리에서](app-insights-analytics.md) 이와 같은:

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

각 레코드를 유지 `itemCount` hello 원래 레코드 수를 나타내는 것 같으면 too1 + 이전 레코드는 삭제 된 hello 수를 나타냅니다. 


## <a name="automation"></a>Automation

Azure 리소스 관리를 사용 하 여 스크립트 tooset hello 가격 계획을 작성할 수 있습니다. [방법을 알아보세요](app-insights-powershell.md#price).

## <a name="limits-summary"></a>제한 요약
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>다음 단계

* [샘플링](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/

