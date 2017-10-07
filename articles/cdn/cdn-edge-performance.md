---
title: "Azure CDN에서에 지 노드 성능 aaaAnalyze | Microsoft Docs"
description: "Microsoft Azure CDN에서 에지 노드 성능을 분석합니다. 가장자리 성능 분석 hello CDN에 대 한 세부적인 정보 트래픽 및 대역폭 사용량을 제공합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>Microsoft Azure CDN에서 에지 노드 성능 분석
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>개요
가장자리 성능 분석 hello CDN에 대 한 세부적인 정보 트래픽 및 대역폭 사용량을 제공합니다. 이 정보 자산 캐시 및 배달 tooyour 클라이언트 되는 방법에 대 한 정보 toogain 수 있게 해 주는 사용된 toogenerate 추세 통계 수 있습니다. 이렇게 하면 tooform 어떻게 콘텐츠와 toodetermine toooptimize hello 배달 어떤 문제에 전략 해야 toobetter 활용 hello CDN은 해결 했습니다. 따라서 수 tooimprove 데이터 배달 성능 수 뿐만 아니라이 수 tooreduce CDN 비용을 수 있습니다.

> [!NOTE]
> 모든 보고서는 날짜/시간을 지정할 때 UTC/GMT 표기법을 사용합니다.
> 
> 

## <a name="reports-and-log-collection"></a>보고서 및 로그 수집
으로 보고서를 생성할 수 있습니다 전에 hello 가장자리 성능 분석 모듈에 의해 CDN 활동 데이터를 수집 해야 합니다. 이 수집 프로세스는 하루에 대해서도 설명 hello 활동 hello 이전 날짜에 발생 한 후에 발생 합니다. 보고서의 통계, 처리 된 것을 의미 하지는 않습니다 hello 시 hello 날의 통계의 샘플을 나타내는이 즉 hello 완전 한 hello에 대 한 데이터 집합 현재 날짜를 포함 합니다. 이러한 보고서의 기본 기능은 hello는 tooassess 성능. 대금 청구 또는 정확한 숫자 통계를 위해서는 사용하지 않아야 합니다.

> [!NOTE]
> 가장자리 성능 분석 보고서가 생성 하는 hello 원시 데이터는 적어도 90 일 동안 사용할 수 있습니다.
> 
> 

## <a name="dashboard"></a>대시보드
hello 가장자리 성능 분석 대시보드 차트 및 통계를 통해 현재 및 과거 CDN 트래픽을 추적합니다. 계정에 대해 CDN 트래픽의 hello 성능에이 대시보드 toodetect 최근 및 장기 추세를 사용 합니다.

이 대시보드는 다음으로 구성됩니다.

* 주요 메트릭 및 추세의 hello 시각화를 허용 하는 대화형 차트.
* 주요 메트릭 및 추세에 대한 장기적인 패턴 감각을 제공하는 타임라인
* CDN 네트워크에서 사이트 트래픽이 어떻게 개선되는지를 전체 성능, 사용 현황 및 효율성으로 측정한 주요 메트릭 및 통계 정보

### <a name="accessing-hello-edge-performance-dashboard"></a>Hello 가장자리 성능 대시보드 액세스
1. Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
2. 마우스 포인터를 놓고 hello **분석** 누른 마우스 포인터를 놓고 hello **가장자리 성능 분석** 플라이 아웃입니다.  **대시보드**를 클릭합니다.
   
    hello 가장자리 노드 분석 대시보드 표시 됩니다.

### <a name="chart"></a>차트
hello 대시보드를 바로 아래에 나타나는 hello 타임 라인에서 선택한 기간 hello를 통해 한 메트릭을 추적 하는 차트를 포함 합니다.  2 년간 CDN 활동의 toohello를 그래프로 표시 되는 일정을 hello 차트 바로 아래에 표시 됩니다.

#### <a name="using-hello-chart"></a>Hello 차트를 사용 하 여
* 기본적으로 지난 30 일 동안 hello에 대 한 hello 캐시 효율성 속도 차트로 작성 됩니다.
* 이 차트는 매일 수집된 데이터에서 생성됩니다.
* Hello 선 그래프에서 날짜를 가리키면 해당 날짜에 hello 메트릭의 hello 및 날짜 값을 표시 합니다.
* 강조 표시 주말 tootoggle 오버레이 hello 차트에 주말 나타내는 밝은 회색 세로 막대를 클릭 합니다. 이 유형의 오버레이는 주말 동안의 트래픽 패턴을 식별하는 데 유용합니다.
* 1 년 전 보기 tootoggle 오버레이 이전 hello 클릭 하 여 hello 통해 활동을 연도 기간 hello 차트에 동일한 시간입니다. 이 유형의 비교를 통해 장기 CDN 사용 패턴에 대한 이해를 넓힐 수 있습니다. hello 차트의 오른쪽 상단 모서리 hello hello 각 선 그래프 색상 코드를 지정 하는 범례가 포함 되어 있습니다.

#### <a name="updating-hello-chart"></a>Hello 차트를 업데이트합니다.
* 시간 범위 hello 다음 중 하나를 수행 합니다.:
  * Hello 타임 라인에서 hello 원하는 지역을 선택 합니다. hello 차트 toohello 특정 기간에 해당 하는 데이터로 업데이트 됩니다.
  * 차트 toodisplay tooa 최대 2 년을 사용 가능한 모든 기록 데이터 hello 하는 두 번 클릭 합니다.
* 메트릭: 다음 원하는 toohello 메트릭을 나타나는 hello 차트 아이콘을 클릭 합니다. hello 차트 및 hello 타임 라인 hello 해당 메트릭에 대 한 데이터로 새로 고쳐집니다.

### <a name="key-metrics-and-statistics"></a>주요 메트릭 및 통계
#### <a name="efficiency-metrics"></a>효율성 메트릭
hello 이러한 메트릭의 목적은 toosee 캐시 효율성을 향상 시킬 수 있는지 여부를입니다. 캐시 효율성이에서 파생 된 hello 주요 이점은 다음과 같습니다.

* 야기할 수 있는 hello 원본 서버의 로드 감소:
  * 웹 서버 성능 향상
  * 운영 비용 절감
* 더 많은 요청이 hello CDN에서 직접 제공 하므로 데이터 배달 가속을 향상 되었습니다.

| 필드 | 설명 |
| --- | --- |
| 캐시 효율성 |전송 되는 데이터의 캐시에서 제공 된 hello 백분율을 나타냅니다. 이 메트릭 측정 때 캐시 된 버전의 hello 콘텐츠 hello CDN (에 지 서버) toorequesters (예: 웹 브라우저)에서 직접 처리 된 요청 |
| 적중률 |캐시에서 처리 된 요청의 hello 비율을 나타냅니다. 이 메트릭 측정 때 캐시 된 버전의 hello hello CDN (에 지 서버) toorequesters (예: 웹 브라우저)에서 직접 처리 된 콘텐츠를 요청 했습니다. |
| % 원격 바이트 - No Cache 구성 |원본 서버 toohello hello 바이패스 캐시 기능 (HTTP 규칙 엔진)의 결과로 캐시 되지 것입니다 CDN (에 지 서버)에서 제공 된 트래픽 hello 백분율을 나타냅니다. |
| % 원격 바이트 - 만료된 캐시 |오래 된 콘텐츠 유효성 재검사 결과로 원본 서버 toohello CDN (에 지 서버)에서 제공 된 트래픽 hello 백분율을 나타냅니다. |

#### <a name="usage-metrics"></a>사용 현황 메트릭
이러한 메트릭의 목적은 hello은 비용 가공 조치를 수행 하는 hello에 대 한 tooprovide 한 정보입니다.

* Hello CDN 통해 운영 비용을 최소화 합니다.
* 캐시 효율성 및 압축을 통해 CDN 지출 감소

> [!NOTE]
> 트래픽 볼륨 숫자 트래픽을 대량 고객에 대 한 트래픽 당 총 hello의 일부만 표시 될 수 있습니다의 비율과 백분율을 계산에 사용 된 것을 나타냅니다.
> 
> 

| 필드 | 설명 |
| --- | --- |
| 평균 바이트 출력 |Hello 평균 hello CDN (에 지 서버) toohello 요청자 (예: 웹 브라우저)에서 제공 하는 각 요청에 대해 전송 된 바이트 수를 나타냅니다. |
| No Cache 구성 바이트 비율 |Hello CDN (에 지 서버) toohello 요청자에 게 (예: 웹 브라우저) toohello 바이패스 캐시 기능 때문에 캐시 되지 것입니다는에서 제공 하는 트래픽의 hello 백분율을 나타냅니다. |
| 압축된 바이트 비율 |압축된 된 형식으로 hello CDN (에 지 서버) toorequesters (예: 웹 브라우저)에서 보낸 트래픽은의 hello 백분율을 나타냅니다. |
| 바이트 출력 |Hello 양을 hello CDN (에 지 서버) toohello 요청자 (예: 웹 브라우저)에서 전달 된 바이트 단위로 데이터를 나타냅니다. |
| 바이트 입력 |Hello 양을 데이터 (예: 웹 브라우저) 요청자 toohello CDN (에 지 서버)에서 보낸 바이트 단위로 나타냅니다. |
| 바이트 원격 |CDN 및 고객 원본 서버 toohello CDN (에 지 서버)에서 보낸 바이트 단위로 데이터의 hello 양을 나타냅니다. |

#### <a name="performance-metrics"></a>성능 메트릭
이러한 메트릭의 hello 목적은 tootrack 트래픽의 대 한 전체 CDN 성능을 합니다.

| 필드 | 설명 |
| --- | --- |
| 전송 속도 |Hello 평균 속도를 hello CDN tooa 요청자에서 전송 된 콘텐츠를 나타냅니다. |
| 기간 |Hello 평균 시간을 나타냅니다. 밀리초 단위로 걸리는 toodeliver 자산 tooa 요청자 (예: 웹 브라우저). |
| 압축된 요청률 |압축된 된 형식으로 hello CDN (에 지 서버) toohello 요청자 (예: 웹 브라우저)에서 전달 된 적중 횟수의 hello 백분율을 나타냅니다. |
| 4xx 오류율 |4xx 상태 코드를 생성 하는 적중 항목의 hello 백분율을 나타냅니다. |
| 5xx 오류율 |5xx 상태 코드를 생성 하는 적중 항목의 hello 백분율을 나타냅니다. |
| 적중 횟수 |Hello CDN 콘텐츠에 대 한 요청 수를 나타냅니다. |

#### <a name="secure-traffic-metrics"></a>보안 트래픽 메트릭
hello 이러한 메트릭의 목적은 HTTPS 트래픽에 대 한 tootrack CDN 성능입니다.

| 필드 | 설명 |
| --- | --- |
| 보안 캐시 효율성 |캐시에서 처리 된 HTTPS 요청을 전송 되는 데이터의 hello 백분율을 나타냅니다. 이 메트릭은 요청 될 때 캐시 된 버전의 hello 콘텐츠 hello CDN (에 지 서버) toorequesters (예: 웹 브라우저)에서 직접 처리 된 HTTPS를 통해 측정 합니다. |
| 보안 전송 속도 |HTTPS를 통한 hello 평균 속도를 hello CDN (에 지 서버) toorequesters (예: 웹 서버)에서 전송 된 콘텐츠를 나타냅니다. |
| 평균 보안 기간 |Hello 평균 시간을 나타냅니다. 밀리초 단위로 걸리는 toodeliver 자산 tooa 요청자 (예: 웹 브라우저) HTTPS를 통한 합니다. |
| 보안 적중 횟수 |Hello 수가 CDN 콘텐츠에 대 한 HTTPS 요청을 나타냅니다. |
| 보안 바이트 출력 |Hello hello CDN (에 지 서버) toohello 요청자 (예: 웹 브라우저)에서 전송 된 바이트에 HTTPS 트래픽 양을 나타냅니다. |

## <a name="reports"></a>보고서
이 모듈의 각 보고서에는 다양한 메트릭 유형(예: HTTP 상태 코드, 캐시 상태 코드, 요청 URL 등)에 대한 차트와 대역폭 및 트래픽 사용 현황에 대한 통계 정보가 포함됩니다. 이 정보에 사용 되는 toodelve tooyour 클라이언트와 toofine 조정 CDN 동작 tooimprove 데이터 배달 성능 콘텐츠 제공 하는 방법을를 자세하게 수 있습니다.

### <a name="accessing-hello-edge-performance-reports"></a>Hello 가장자리 성능 보고서에 액세스
1. Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
2. 마우스 포인터를 놓고 hello **분석** 누른 마우스 포인터를 놓고 hello **가장자리 성능 분석** 플라이 아웃입니다.  **HTTP 큰 개체**를 클릭합니다.
   
    hello 가장자리 노드 분석 보고서 화면이 표시 됩니다.

| 보고서 | 설명 |
| --- | --- |
| 일일 요약 |있습니다 tooview 트래픽 일별로 지정 된 기간 동안. 이 그래프의 각 막대는 특정 날짜를 나타냅니다. hello 막대의 hello 크기는 해당 날짜에 발생 한 횟수가 hello 총 수를 나타냅니다. |
| 시간별 요약 |있습니다 tooview 시간별 트래픽 추세를 지정 된 기간 동안. 이 그래프에서 각 막대는 특정 날짜에서 한 시간을 나타냅니다. hello 막대의 hello 크기는 해당 시간 동안 발생 한 횟수가 hello 총 수를 나타냅니다. |
| 프로토콜 |Hello HTTP 및 HTTPS 프로토콜 간의 트래픽 hello 분석 결과 표시합니다. 도넛형 차트는 각 유형의 프로토콜에 대해 발생 한 횟수가 hello 백분율을 나타냅니다. |
| HTTP 메서드 |Tooget는 HTTP 메서드의 빠른 의미는 사용 하면 사용 되는 toorequest 데이터 되 고 있습니다. 일반적으로 hello 가장 일반적으로 HTTP 요청 메서드는 GET, HEAD, 및 POST입니다. 도넛형 차트 HTTP 요청 메서드의 각 형식에 대해 발생 한 횟수가 hello 백분율을 나타냅니다. |
| URL |Hello 상위 10 개의 요청 된 Url을 표시 하는 그래프를 포함 합니다. 각 URL에 대한 막대가 표시됩니다. hello 막대의 높이 hello hello 보고서에서 포함 특정 URL에 hello 시간 범위에 대해 생성 되는 적중 항목 수를 나타냅니다. Hello 상위 100에 대 한 통계 요청 Url이이 그래프 바로 아래에 표시 됩니다. |
| CNAME |보고서의 hello 시간 범위 동안 hello 상위 10 개의 사용 CNAMEs toorequest 자산을 표시 하는 그래프를 포함 합니다. Hello 상위 100에 대 한 통계 요청 Cname이이 그래프 바로 아래에 표시 됩니다. |
| 원본 |Hello 상위 10 개의 CDN 또는 고객 원본 서버는 지정 된 기간 동안 요청 된 자산을 표시 하는 그래프를 포함 합니다. Hello 상위 100에 대 한 통계 요청 CDN 또는 고객 원본 서버는이 그래프 바로 아래 표시 됩니다. 고객 원본 서버 hello 디렉터리 이름 옵션에에서 정의 된 hello 이름으로 식별 됩니다. |
| 지역 POP |얼마 만큼의 트래픽이 특정 상호 접속 위치(POP)를 통해 라우팅되는지를 보여줍니다. hello 3 자 약어에 CDN POP을 나타냅니다. |
| 클라이언트 |Hello 상위 10 명의 요청한 클라이언트에 자산 지정 된 기간 동안 표시 되는 그래프를 포함 합니다. 모든 요청에서 발생 하는 hello 동일 hello이이 보고서를 위해 IP 주소에서 hello toobe 것으로 간주 됩니다 동일한 클라이언트입니다. 상위 100 명의 클라이언트 hello에 대 한 통계는이 그래프 바로 아래에 표시 됩니다. 이 보고서는 최상위 클라이언트에 대한 다운로드 활동 패턴을 결정하는 데 유용합니다. |
| 캐시 상태 |개선 하기 위한 접근 방식을 표시할 수 있는 캐시 동작에 대 한 자세한 분석을 제공 hello 전체적인 최종 사용자 경험 합니다. Hello 보다 빠른 성능을 캐시 적중 횟수에 도달할 이후 만료 된 캐시 적중 수 및 캐시 누락 수를 최소화 하 여 데이터 배달 속도 최적화할 수 있습니다. |
| NONE 세부 정보 |Hello를 캐시 콘텐츠 새로 고침 지정 된 기간 동안 선택 하지 않은 자산에 대 한 상위 10 개의 Url을 표시 하는 그래프를 포함 합니다. 이러한 유형의 자산에 대 한 hello 상위 100 Url에 대 한 통계는이 그래프 바로 아래에 표시 됩니다. |
| CONFIG_NOCACHE 세부 정보 |Toohello 고객의 CDN 구성 때문에 캐시 되지 않은 자산에 대 한 hello 상위 10 개의 Url을 표시 하는 그래프를 포함 합니다. 이러한 유형의 자산 hello 원본 서버에서 직접 처리 된 합니다. 이러한 유형의 자산에 대 한 hello 상위 100 Url에 대 한 통계는이 그래프 바로 아래에 표시 됩니다. |
| UNCACHEABLE 세부 정보 |Hello toorequest 헤더 데이터 인해 캐시 될 수 있는 자산에 대 한 상위 10 개의 Url을 표시 하는 그래프를 포함 합니다. 이러한 유형의 자산에 대 한 hello 상위 100 Url에 대 한 통계는이 그래프 바로 아래에 표시 됩니다. |
| TCP_HIT 세부 정보 |캐시에서 즉시 처리 되는 자산에 대 한 hello 상위 10 개의 Url을 표시 하는 그래프를 포함 합니다. 이러한 유형의 자산에 대 한 hello 상위 100 Url에 대 한 통계는이 그래프 바로 아래에 표시 됩니다. |
| TCP_MISS 세부 정보 |Hello TCP_MISS 상태의 캐시 하는 자산에 대 한 상위 10 개의 Url을 표시 하는 그래프를 포함 합니다. 이러한 유형의 자산에 대 한 hello 상위 100 Url에 대 한 통계는이 그래프 바로 아래에 표시 됩니다. |
| TCP_EXPIRED_HIT 세부 정보 |Hello hello POP에서 직접 처리 된 오래 된 자산에 대 한 상위 10 개의 Url을 표시 하는 그래프를 포함 합니다. 이러한 유형의 자산에 대 한 hello 상위 100 Url에 대 한 통계는이 그래프 바로 아래에 표시 됩니다. |
| TCP_EXPIRED_MISS 세부 정보 |Hello를 새 버전에 toobe hello 원본 서버에서 검색 하는 오래 된 자산에 대 한 상위 10 개의 Url을 표시 하는 그래프를 포함 합니다. 이러한 유형의 자산에 대 한 hello 상위 100 Url에 대 한 통계는이 그래프 바로 아래에 표시 됩니다. |
| TCP_CLIENT_REFRESH_MISS 세부 정보 |클라이언트 hello tooa 아니요 캐시 요청 인해 원본 서버에서 검색 된 자산에 대 한 hello 상위 10 개의 Url을 표시 하는 가로 막대형 차트를 포함 합니다. 이러한 종류의 요청에 대 한 hello 상위 100 Url에 대 한 통계는이 차트 바로 아래에 표시 됩니다. |
| 클라이언트 요청 유형 |HTTP 클라이언트 (예: 브라우저)에 한 요청의 hello 유형을 나타냅니다. 이 보고서는 요청 처리 되 고 toohow 의미 있는 기능을 제공 하는 도넛형 차트에 포함 됩니다. 각 요청 유형에 대 한 정보를 캡슐화 된 트래픽과 대역폭 hello 차트 아래에 표시 됩니다. |
| 사용자 에이전트 |Hello 상위 10 개의 사용자 에이전트 toorequest 우리의 CDN 통해 콘텐츠를 표시 하는 막대 그래프를 포함 합니다. 일반적으로 사용자 에이전트는 웹 브라우저, 미디어 플레이어 또는 휴대폰 브라우저입니다. Hello 상위 100 사용자 에이전트에 대 한 통계는이 차트 바로 아래에 표시 됩니다. |
| 참조 페이지 |Hello 상위 10 명의 참조 페이지 toocontent 우리의 CDN을 통해 액세스를 표시 하는 막대 그래프를 포함 합니다. 일반적으로 참조 하는 페이지는 hello 웹 페이지 또는 tooyour 콘텐츠를 연결 하는 리소스의 hello URL입니다. Hello 상위 100 참조 페이지에 대 한 hello 그래프 아래 세부 정보가 제공 됩니다. |
| 압축 형식 |요청된 자산이 에지 서버에 의해 압축되는지 여부를 자세히 분석한 도넛형 차트를 포함합니다. 압축 된 자산의 hello 백분율은 사용 되는 압축 hello 유형별 나누어집니다. 각 압축 유형 및 상태에 대 한 hello 그래프 아래 세부 정보가 제공 됩니다. |
| 파일 형식 |사용자 계정에 대 한 우리의 CDN을 통해 요청 된 hello 상위 10 개의 파일 종류를 표시 하는 막대 그래프를 포함 합니다. 이 보고서의 hello 위해서 파일 형식을 hello 자산 파일 이름 확장명으로 정의 되어 있고 인터넷 미디어 유형 (예:.html \[텍스트/html\],.htm \[텍스트/html\],.aspx \[텍스트/html\]등.). Hello 상위 100 파일 종류에 대 한 hello 그래프 아래 세부 정보가 제공 됩니다. |
| 고유한 파일 |지정 된 기간 동안 특정 한 날에 요청 된 고유 자산 hello 총 수를 표시 하는 그래프를 포함 합니다. |
| 토큰 인증 요약 |요청된 자산이 토큰 기반 인증으로 보호되는지에 대한 빠른 개요를 제공하는 원형 차트를 포함합니다. 자산 보호는 인증 시도의 toohello 결과 따라 hello 차트에 표시 됩니다. |
| 토큰 인증 거부 세부 정보 |Tooview hello 상위 10 개 요청 자가 tooToken 기반 인증으로 인해 거부를 허용 하는 막대 그래프를 포함 합니다. |
| HTTP 응답 코드 |Hello HTTP 상태 코드의 한 분석을 제공 (예: 200 OK가 403 등 404 찾을 수 없음, 사용할 수 없습니다) tooyour HTTP 클라이언트의에 지 서버에서 전달 된입니다. 원형 차트를 사용 하면 tooquickly 자산 처리 된 방법을 평가 합니다. Hello 그래프 아래의 각 응답 코드에 대 한 자세한 통계 데이터가 제공 됩니다. |
| 404 오류 |요청을 허용 하 있습니다 tooview hello 상위 10 개의 404 찾을 수 없음 응답 코드가 발생 하는 막대 그래프를 포함 합니다. |
| 403 오류 |요청을 허용 하 있습니다 tooview hello 상위 10 개의 403 사용 권한 없음 응답 코드가 발생 하는 막대 그래프를 포함 합니다. 403 사용 권한 없음 응답 코드는 POP의 고객 원본 서버 또는 에지 서버에서 요청을 거부하면 발생합니다. |
| 4xx 오류 |요청을 허용 하 있습니다 tooview hello 상위 10 개의 응답 코드가 400 hello 범위에서 발생 하는 막대 그래프를 포함 합니다. 이 보고서에서 제외되는 항목은 403 찾을 수 없음 및 404 사용 권한 없음 응답 코드입니다. 일반적으로 4xx 응답 코드는 클라이언트 오류로 인해 요청이 거부되면 발생합니다. |
| 504 오류 |요청을 허용 하 있습니다 tooview hello 상위 10 개의 504 게이트웨이 시간 초과 응답 코드가 발생 하는 막대 그래프를 포함 합니다. 504 게이트웨이 시간 초과 응답 코드는 HTTP 프록시 하는 동안 다른 서버와 toocommunicate 시간 초과가 발생 하는 경우에 발생 합니다. 504 게이트웨이 시간 초과 응답 코드 hello 경우 모두 우리의 cdn에 지 서버 고객 원본 서버와 통신을 없습니다 tooestablish 때 일반적으로 발생 합니다. |
| 502 오류 |요청을 허용 하 있습니다 tooview hello 상위 10 개의 502 잘못 된 게이트웨이 응답 코드가 발생 하는 막대 그래프를 포함 합니다. 502 잘못된 게이트웨이 응답 코드는 서버와 HTTP 프록시 사이 HTTP 프로토콜 오류가 발생하는 경우 발생합니다. 502 잘못 된 게이트웨이 응답 코드 hello 경우 모두 우리의 cdn 고객 원본 서버에 잘못 된 응답 tooan 지 서버를 반환 하는 경우 일반적으로 발생 합니다. 구문 분석할 수 없거나 완료되지 않은 응답은 유효하지 않습니다. |
| 5xx 오류 |요청을 허용 하 있습니다 tooview hello 상위 10 개의 응답 코드가 500 hello 범위에서 발생 하는 막대 그래프를 포함 합니다.  이 보고서에서 제외되는 항목은 502 잘못된 게이트웨이 및 504 게이트웨이 시간 초과 응답 코드입니다. |

## <a name="see-also"></a>참고 항목
* [Azure CDN 개요](cdn-overview.md)
* [Microsoft Azure CDN의 실시간 통계](cdn-real-time-stats.md)
* [Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의](cdn-rules-engine.md)
* [고급 HTTP 보고서](cdn-advanced-http-reports.md)

