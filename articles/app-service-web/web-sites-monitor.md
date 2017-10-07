---
title: "Azure 앱 서비스에서 앱 aaaMonitor | Microsoft Docs"
description: "방법을 사용 하 여 Azure 앱 서비스에서 toomonitor 앱 hello Azure 포털에 알아봅니다."
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a>방법: Azure App Service에서 앱 모니터링
[앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714) hello에 기본 제공된 모니터링 기능을 제공 [Azure 포털](https://portal.azure.com)합니다.
Hello 기능 tooreview 여기에 **할당량** 및 **메트릭** hello를 설정 하는 앱 서비스 계획 뿐만 아니라 응용 프로그램에 대 한 **경고** 및 심지어 **크기조정** 이러한 메트릭을 기반으로 자동으로 합니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a>할당량 및 메트릭 이해
### <a name="quotas"></a>할당량
앱 서비스에서 호스팅되는 응용 프로그램은 주제 toocertain *제한* 에 리소스를 사용할 수 있습니다. hello 제한에서 정의 된 hello **앱 서비스 계획** hello 앱과 연결 된입니다.

Hello 응용 프로그램에서 호스팅되는 경우는 **무료** 또는 **Shared** hello 앱 צ ְ ײ hello 리소스에 대 한 hello도 정의한 다음 계획 **할당량**합니다.

Hello 응용 프로그램에서 호스팅되는 경우는 **기본**, **표준** 또는 **프리미엄** hello 설정한 hello 제한을 사용 하 여 hello 리소스에 대 한 다음 계획 **크기** (소형, 중형, 대형) 및 **인스턴스 수를** (1, 2, 3,...)의 hello **앱 서비스 계획**합니다.

**무료** 또는 **공유** 앱에 대한 **할당량**은 다음과 같습니다.

* **CPU(Short)**
  * 5분 간격으로 이 응용 프로그램에 대해 허용되는 CPU의 양입니다. 이 할당량은 5분마다 재설정됩니다.
* **CPU(Day)**
  * 하루에 이 응용 프로그램에 대해 허용되는 총 CPU 양입니다. 이 할당량은 자정 UTC에 24시간마다 재설정됩니다.
* **메모리**
  * 이 응용 프로그램에 대해 허용되는 총 메모리 양입니다.
* **대역폭**
  * 하루에 이 응용 프로그램에 대해 허용되는 나가는 총 대역폭 양입니다.
    이 할당량은 자정 UTC에 24시간마다 재설정됩니다.
* **파일 시스템**
  * 허용되는 총 저장소 양입니다.

만 할당량 적용 가능한 tooapps에 호스팅된 hello **기본**, **표준** 및 **프리미엄** 계획은 **Filesystem**합니다.

Hello 특정 할당량, 제한 및 다른 응용 프로그램 서비스 Sku hello를 사용할 수 있는 기능에 대 한 자세한 내용은 여기에서 찾을 수 있습니다: [Azure 구독 서비스 제한](../azure-subscription-service-limits.md#app-service-limits)

#### <a name="quota-enforcement"></a>할당량 적용
사용법에 응용 프로그램이 초과 hello **CPU (short)**, **CPU (일)**, 또는 **대역폭** hello 할당량이 다시 설정 될 때까지 할당량 다음 hello 응용 프로그램을 중지 합니다. 이 시간 중에는 들어오는 모든 요청에서 **HTTP 403**이 발생합니다.
![][http403]

하는 경우 응용 프로그램 hello **메모리** 할당량이 초과 되 면 다음 hello 응용 프로그램 다시 시작 됩니다.

경우 hello **Filesystem** 할당량이 초과 되 면 다음 쓰기 toologs 작성을 포함 하 여 작업이 실패 합니다.

App Service 계획을 업그레이드하여 앱에서 할당량을 증가 또는 제거할 수 있습니다.

### <a name="metrics"></a>메트릭
**메트릭** hello 앱 또는 앱 서비스 계획의 동작에 대 한 정보를 제공 합니다.

에 대 한 프로그램 **응용 프로그램**, 사용할 수 있는 메트릭을 hello:

* **평균 응답 시간**
  * ms에서 hello 앱 tooserve 요청에 걸리는 평균 시간을 hello 합니다.
* **평균 메모리 작업 집합**
  * hello hello 앱에서 사용 하는 Mib에는 메모리의 평균 크기입니다.
* **CPU 시간**
  * hello CPU 양이 hello 앱에서 사용 하는 시간 (초)에 있습니다. 이 메트릭에 대한 자세한 내용은 [CPU 시간 및 CPU 비율](#cpu-time-vs-cpu-percentage)을 참조하세요.
* **데이터 입력**
  * hello Mib에는 앱에서 사용 하는 들어오는 대역폭의 hello 양입니다.
* **데이터 출력**
  * hello Mib에는 앱에서 사용 하는 나가는 대역폭의 hello 양입니다.
* **Http 2xx**
  * 결과로 나타나는 Http 상태 코드가 200 이상 300 미만인 요청 수입니다.
* **Http 3xx**
  * 결과로 나타나는 Http 상태 코드가 300 이상 400 미만인 요청 수입니다.
* **Http 401**
  * 결과로 HTTP 401 상태 코드가 나타나는 요청의 수입니다.
* **Http 403**
  * 결과로 HTTP 403 상태 코드가 나타나는 요청의 수입니다.
* **Http 404**
  * 결과로 HTTP 404 상태 코드가 나타나는 요청의 수입니다.
* **Http 406**
  * 결과로 HTTP 406 상태 코드가 나타나는 요청의 수입니다.
* **Http 4xx**
  * 결과로 나타나는 Http 상태 코드가 400 이상 500 미만인 요청 수입니다.
* **Http 서버 오류**
  * 결과로 나타나는 Http 상태 코드가 500 이상 600 미만인 요청 수입니다.
* **메모리 작업 집합**
  * 현재 Mib에 hello 앱에서 사용 하는 메모리 양입니다.
* **요청**
  * 결과 HTTP 상태 코드에 관계 없이 총 요청 수입니다.

에 대 한 프로그램 **앱 서비스 계획**, 사용할 수 있는 메트릭을 hello:

> [!NOTE]
> App Service 계획 메트릭은 **기본**, **표준** 및 **프리미엄** SKU의 계획에만 사용할 수 있습니다.
> 
> 

* **CPU 비율**
  * hello 계획의 모든 인 스턴에서 사용 되는 평균 CPU hello입니다.
* **메모리 비율**
  * hello 평균 메모리 hello 계획의 모든 인 스턴에서 사용 합니다.
* **데이터 입력**
  * hello 평균 들어오는 대역폭 hello 계획의 모든 인 스턴에서 사용 되는입니다.
* **데이터 출력**
  * hello 평균 나가는 hello 계획의 모든 인 스턴에서 사용 되는 대역폭입니다.
* **디스크 큐 길이**
  * hello 평균 수 읽기 및 쓰기의 대기 중인 요청을 저장소에 합니다. 디스크 큐 길이 tooexcessive 디스크 I/O 인해 속도 저하 될 수 있는 응용 프로그램을 나타냅니다.
* **Http 큐 길이**
  * hello 하기 전의 toosit hello 큐에 처리 되는 HTTP 요청의 평균 수입니다. HTTP 큐 길이 값이 높거나 증가하면 계획이 과부하 상태에 있음을 나타냅니다.

### <a name="cpu-time-vs-cpu-percentage"></a>CPU 시간 및 CPU 비율
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

CPU 사용량을 반영하는 두 가지 메트릭이 있습니다. **CPU 시간** 및 **CPU 비율**

**CPU 시간** 에서 호스트 되는 앱에 대해 유용 **무료** 또는 **Shared** 자신의 할당액 중 하나는 hello 앱에서 사용 하는 CPU 시간 (분)에 정의 되어 있으므로 계획 합니다.

**CPU 백분율** hello에 다른 포인터는 유용한에서 호스트 되는 앱에 대해 **기본**, **표준** 및 **프리미엄** 확장할 수 있습니다 이후 계획 및이 메트릭은 상태 hello의 모든 인 스턴에서 전체 사용량.

## <a name="metrics-granularity-and-retention-policy"></a>메트릭 세분성 및 보존 정책
응용 프로그램 및 응용 프로그램 서비스 계획에 대 한 메트릭을 기록 되어 hello로 hello 서비스에 의해 집계 세분성 및 보존 정책에 따라:

* **분** 세분성 메트릭은 **48시간** 동안 보존됩니다.
* **시** 세분성 메트릭은 **30일** 동안 보존됩니다.
* **일** 세분성 메트릭은 **90일** 동안 보존됩니다.

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a>할당량 및 hello Azure 포털에서에서 메트릭을 모니터링 합니다.
다른 hello hello 상태를 검토할 수 **할당량** 및 **메트릭** hello에서 응용 프로그램에 영향을 주는 [Azure 포털](https://portal.azure.com)합니다.

![][quotas]
**할당량**은 설정>**할당량** 아래에서 찾을 수 있습니다. hello UX 검토할 수 있습니다. (1) hello 할당량 이름, (2)의 다시 설정 간격, (3)의 현재 한도 및 (4) 현재 값입니다.

![][metrics]
**메트릭** hello 리소스 블레이드에서 직접 액세스할 수 있습니다. 하는 hello 차트를 사용자 지정할 수도 있습니다: (1) **클릭** ,을 선택 (2) **차트 편집**합니다.
여기에서 hello (3)을 변경할 수 있습니다 **시간 범위**, (4) **차트 종류**, (5) 및 **메트릭** toodisplay 합니다.  

[서비스 메트릭 모니터링](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)에서 메트릭에 대해 자세히 알아볼 수 있습니다.

## <a name="alerts-and-autoscale"></a>경고 및 자동 크기 조정
메트릭 tooalerts,이 대 한 자세한 toolearn 연결할 수는 앱 또는 앱 서비스 계획에 대 한 참조 [경고 알림 받기](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

기본, 표준 또는 프리미엄 App Service 계획에 호스팅된 앱 서비스 앱은 **자동 크기 조정**을 지원합니다. 이렇게 하면 있습니다 tooconfigure 규칙을 앱 서비스 계획 메트릭을 모니터링 하 고 거 나 낮출 수 필요에 따라 추가 리소스를 제공 하는 hello 인스턴스 수 또는 저장 하는 중 money hello 응용 프로그램은 과도 하 게 프로 비전 하는 경우. 여기에 자동 크기 조정에 대 한 자세히 알아볼 수 있습니다: [어떻게 tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) 및 여기 [Azure 모니터 자동 크기 조정에 대 한 유용한 정보](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)

> [!NOTE]
> Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)앱 서비스의 수명이 짧은 스타터 웹 응용 프로그램 즉시 만들 수 있는, 합니다. 신용 카드는 필요하지 않으며 약정도 필요하지 않습니다.
> 
> 

## <a name="whats-changed"></a>변경된 내용
* 웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
