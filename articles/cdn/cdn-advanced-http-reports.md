---
title: "Azure CDN을 사용 하 여 aaaAnalyze 사용량 통계 고급 HTTP 보고서 | Microsoft Docs"
description: "Toocreate Microsoft Azure CDN에서 HTTP 보고서 고급 하는 방법에 대해 알아봅니다. 이러한 보고서는 CDN 활동에 대한 자세한 정보를 제공합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>Azure CDN 고급 HTTP 보고서를 사용하여 사용 현황 통계 분석
## <a name="overview"></a>개요
이 문서에서는 Microsoft Azure CDN에서 고급 HTTP 보고에 대해 설명합니다. 이러한 보고서는 CDN 활동에 대한 자세한 정보를 제공합니다.

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>고급 HTTP 보고서 액세스
1. Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
2. 마우스 포인터를 놓고 hello **분석** 누른 마우스 포인터를 놓고 hello **HTTP 보고서 고급** 플라이 아웃입니다.  **HTTP 큰 플랫폼**을 클릭합니다.
   
    ![CDN 관리 포털 - 고급 보고서 메뉴](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    보고서 옵션이 표시됩니다.

## <a name="geography-reports-map-based"></a>지리 보고서(맵 기반)
지도 tooindicate 콘텐츠를 요청 하 고 hello 영역을 이용 하는 다섯 개의 보고서 있습니다. 이러한 보고서는 전 세계 맵, 미국 맵, 캐나다 맵, 유럽 맵 및 아시아 태평양 맵입니다.

각 지도 기반 보고서의 지리적 엔터티 (즉, 국가, 상태 및 시/도) 순위가 해당 지역에서 발생 한 횟수가 toohello 비율에 따라 합니다. 또한 지도는 콘텐츠를 요청 하 고 hello 위치를 시각화 toohelp 제공 됩니다. 이므로 수 toodo 해당 지역의 각 지역에 색 구분 하 여 toohello 양을 수요에 따라 발생 합니다. 밝게 음영 처리된 지역은 콘텐츠에 대한 요구가 낮은 반면, 어둡게 음영 처리된 지역은 콘텐츠에 대한 요구 수준이 높습니다.

각 지역에 대 한 자세한 트래픽 및 대역폭 정보 hello 지도 바로 아래에 제공 됩니다. 이렇게 하면 tooview hello의 총 적중 횟수, 적중 횟수의 hello 백분율, (기가바이트)에서 전송 되는 데이터의 총 hello와 hello 비율의 데이터 파일에 대 한 각 지역입니다. 이러한 각 메트릭에 대한 설명을 확인합니다. 마지막으로 (즉, 국가, 주 또는) 영역 위로 마우스를 가져가면 hello 이름과 hello 백분율 hello 지역에서 발생 한 횟수가 나타납니다 도구 설명으로.

맵 기반 지리 보고서의 각 유형에 대한 간략한 설명이 아래에 제공됩니다.

| 보고서 이름 | 설명 |
| --- | --- |
| 전 세계 맵 |이 보고서는 CDN 콘텐츠에 대 한 tooview hello 전 세계 수요가 있습니다. 각 국가 해당 지역에서 시작 하는 적중 항목의 hello world 지도 tooindicate hello 비율에 색 구분 되어 있습니다. |
| 미국 맵 |이 보고서에서는 미국 hello에 CDN 콘텐츠에 대 한 tooview hello 요구 합니다. 각 상태는이 지도 tooindicate hello 해당 지역에서 시작 된 적중 횟수의 비율에 색이 지정 합니다. |
| 캐나다 맵 |이 보고서는 CDN 콘텐츠 캐나다에서에 대 한 tooview hello 요구가 있습니다. 각 시/도이 지도 tooindicate hello 해당 지역에서 시작 된 적중 횟수의 비율에 색이 지정 합니다. |
| 유럽 맵 |이 보고서는 유럽의 CDN 콘텐츠에 대 한 tooview hello 요구가 있습니다. 이 지도 tooindicate hello 해당 지역에서 시작 된 적중 횟수의 비율에 각 국가 색이 지정 됩니다. |
| 아시아 태평양 맵 |이 보고서는 아시아의 CDN 콘텐츠에 대 한 tooview hello 요구가 있습니다. 이 지도 tooindicate hello 해당 지역에서 시작 된 적중 횟수의 비율에 각 국가 색이 지정 됩니다. |

## <a name="geography-reports-bar-charts"></a>지리 보고서(가로 막대형 차트)
두 개의 추가 보고서 toogeography에 따라 통계 정보를 제공 하는 상위 도시 및 Top 국가 있습니다. 이러한 보고서 순위 도시와 국가, 각각 해당 영역에서 시작 된 적중 toohello 수에 따라 합니다. 이러한 종류의 보고서를 생성 하면 가로 막대형 차트는 상위 10 개의 도시 hello 또는 국가는 특정 플랫폼을 통해 요청 되는 콘텐츠를 나타냅니다. 이 막대형 차트를 사용 하면 있습니다 tooquickly hello 가장 높은 수의 콘텐츠에 대 한 요청 생성 하는 hello 영역을 평가 합니다.

hello 그래프 (y 축)의 왼쪽 hello 방문 횟수 hello 지정 된 영역에서 발생을 나타냅니다. Hello 그래프 (x 축) 바로 아래 개 hello 상위 10 개 지역 각각에 대 한 레이블을 찾을 수 있습니다.

### <a name="using-hello-bar-charts"></a>Hello 가로 막대형 차트를 사용 하 여
* 막대를 마우스로 가리키면 hello 이름과 hello의 총 적중 hello 지역에서 발생 한 도구 설명으로 표시 됩니다.
* hello 도구 설명 위쪽 도시 보고서 hello에 대 한 이름, 시/도 및 국가 약어는 도시를 식별합니다.
* Hello 도시 또는 요청이 시작 된 지역 (예: 시/도)를 확인할 수 없습니다, 알려진 되지 않은 표시 됩니다 것입니다. 이면 hello 국가 알 수 없음, 다음 두 물음표 (즉,??) 표시 됩니다.
* 보고서에는 "Europe" 또는 "아시아/Pacific 지역입니다." hello에 대 한 메트릭을 포함 될 수 있습니다. 이러한 항목은 해당 영역에서 모든 IP 주소에 tooprovide 통계 정보를 아닙니다. 대신에 걸쳐 유럽 또는 아시아/Pacific tooa 특정 도시 또는 국가 대신 IP 주소에서 시작 된 toorequests만 적용 됩니다.

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 가로 막대형 차트를 볼 수 있습니다. Hello의 총 적중, 힌트, hello (기가바이트)에서 전송 되는 데이터 양 비율로 hello 있을 것 및 hello 비율에 대 한 전송 되는 데이터의 hello 상위 250 영역입니다. 이러한 각 메트릭에 대한 설명을 확인합니다.

아래에서 두 가지 유형의 보고서에 대한 간략한 설명을 제공합니다.

| 보고서 이름 | 설명 |
| --- | --- |
| 상위 도시 |이 보고서 도시 해당 지역에서 시작 된 적중 toohello 수에 따라 순위를 지정 합니다. |
| 상위 국가 |이 보고서 국가 해당 지역에서 시작 된 적중 toohello 수에 따라 순위를 지정 합니다. |

## <a name="daily-summary"></a>일일 요약
일별 요약 보고서 hello tooview hello 적중 횟수와 특정 플랫폼을 통해 매일 전송 되는 데이터의 총 수가 있습니다. 이 정보를 사용할 수 있습니다 tooquickly CDN 활동 패턴을 식별 합니다. 예를 들어 이 보고서를 통해 트래픽이 예상보다 높거나 낮게 발생한 날짜를 감지할 수 있습니다.

이러한 종류의 보고서를 생성 하면 가로 막대형 차트는 시각적 표시를 제공 숙련 된 플랫폼별 요청 toohello 양으로 매일 hello를 통해 hello 보고서에 포함 된 기간입니다. Hello 보고서의 각 날짜에 대 한 막대를 표시 하 여 작업 이루어집니다. 예를 들어 "지난 주" 라는 hello 기간을 선택 하면 7 개의 막대가 있는 가로 막대형 차트를 생성 합니다. 각 막대는 hello 해당 날짜에 발생 하는 적중 횟수의 총 수를 나타냅니다.

hello hello 그래프 (y 축)의 왼쪽 방문 횟수에 발생 나타냅니다 hello 지정 된 날짜입니다. Hello 그래프 (x 축) 바로 아래 hello 날짜를 나타내는 레이블을 찾을 수 있습니다 (형식: YYYY-월-일) hello 보고서에 포함 된 각 날짜에 대 한 합니다.

> [!TIP]
> 막대를 마우스로 가리키면 hello의 총 적중 해당 날짜에 발생 한 도구 설명으로 나타납니다.
> 
> 

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 가로 막대형 차트를 볼 수 있습니다. 있습니다 hello 보고서에서 포함 하는 각 날짜에 대 한 hello 총 적중 수 및 hello 크기 (기가바이트)에서 전송 되는 데이터를 찾을 수 있습니다.

## <a name="by-hour"></a>시간별
보고서에서 시간 hello tooview hello 적중 횟수와 시간 단위로 특정 플랫폼을 통해 전송 되는 데이터의 총 수가 있습니다. 이 정보를 사용할 수 있습니다 tooquickly CDN 활동 패턴을 식별 합니다. 예를 들어이 보고서 유용 hello hello 하루 동안 높거나 낮이 예상된 트래픽을 보다 발생할 시간 간격을 검색 합니다.

이러한 종류의 보고서를 생성 하면 가로 막대형 차트는 hello 보고서에 포함 된 기간 hello를 통해 시간 단위로 발생 하는 플랫폼 특정 요청 toohello 양으로 시각적 표시를 제공 합니다. Hello 보고서에서 포함 된 각 시간에 대 한 막대를 표시 하 여 작업 이루어집니다. 예를 들어 24시간 기간을 선택하면 24개의 막대로 가로 막대형 차트를 생성합니다. 각 막대는 hello 해당 시간 동안 발생 하는 적중 횟수의 총 수를 나타냅니다.

hello 그래프 (y 축)의 왼쪽 hello 방문 횟수 hello 지정 된 시간에 발생을 나타냅니다. Hello 그래프 (x 축) 바로 아래 hello 날짜/시간을 나타내는 레이블을 찾을 수 있습니다 (형식: YYYY-월-일 hh: mm) hello 보고서에 포함 된 각 시간에 대 한 합니다. 24 시간 형식을 사용 하 여 시간이 보고 하 고 hello UTC/GMT 표준 시간대를 사용 하 여 지정 된 키를 누릅니다.

> [!TIP]
> 막대를 마우스로 가리키면 hello의 총 적중 해당 시간 동안 발생 한 도구 설명으로 나타납니다.
> 
> 

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 가로 막대형 차트를 볼 수 있습니다. 있습니다 (기가바이트)에서 전송 되는 데이터의 hello 양과 hello 총 적중 수 hello 보고서에서 포함 된 각 시간에 대해 찾을 수 있습니다.

## <a name="by-file"></a>파일별
hello 하 여 파일 보고서를 사용 하면 있습니다 tooview hello 수요와 hello 트래픽 양이 가장 hello에 대 한 특정 플랫폼을 통해 발생 자산을 요청 했습니다. 이러한 종류의 보고서를 생성 하면 시간 간격을 지정 하는 hello를 통해 가로 막대형 차트 hello 상위 10 개의 가장 많이 요청한 자산에 생성 됩니다.

> [!NOTE]
> 이 보고서의 hello 위해서 가장자리 CNAME Url은 변환 된 tootheir 동일한 CDN Url입니다. 이렇게 하면 hello 총 적중 수에 대 한 정확한 집계는 자산과 연결 된 hello CDN 또는 가장자리 사용 하는 CNAME URL toorequest에 관계 없이 있습니다.
> 
> 

hello 그래프 (y 축)의 왼쪽 hello 기간을 지정 하는 hello를 통해 hello 각 자산에 대 한 요청 수를 나타냅니다. Hello 그래프 (x 축) 바로 아래 각 hello 상위 10 개의 요청 된 자산에 대 한 hello 파일 이름을 나타내는 레이블을 찾을 수 있습니다.

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 가로 막대형 차트를 볼 수 있습니다. Hello 다음 각 hello 상위 250 요청 된 자산에 대 한 정보를 있을 것: 상대 경로, 적중 횟수, 적중 횟수의 hello 백분율, hello 크기 (기가바이트)에서 전송 되는 데이터의 총 hello 및 전송 되는 데이터의 hello 백분율입니다.

## <a name="by-file-detail"></a>파일 정보별
파일 세부 정보에서 보고서 hello tooview hello 양을 특정 자산에 대 한 특정 플랫폼을 통해 발생 되는 수요와 hello 트래픽이 있습니다. Hello에이 보고서의 맨은 hello 파일 세부 정보에 대 한 옵션입니다. 이 옵션에는 hello 선택한 플랫폼에서 가장 많이 요청한 자산 목록을 제공합니다. 순서 toogenerate 하 여 파일 세부 정보 보고서에서는 tooselect hello 원하는 자산 hello 파일 세부 정보에 대 한 옵션을에서 해야 합니다. 그 후 가로 막대형 차트는 시간 간격을 지정 하는 hello에 따라 생성 하는 매일 요청 hello 양을 나타냅니다.

hello 그래프 (y 축)의 왼쪽 hello hello 총 자산 특정 날짜에 발생 하는 요청 수를 나타냅니다. Hello 그래프 (x 축) 바로 아래 hello 날짜를 나타내는 레이블을 찾을 수 있습니다 (형식: YYYY-월-일) hello에 대 한 어떤 CDN 요구에 대 한 자산 보고 되었습니다.

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 가로 막대형 차트를 볼 수 있습니다. 있습니다 hello 보고서에서 포함 하는 각 날짜에 대 한 hello 총 적중 수 및 hello 크기 (기가바이트)에서 전송 되는 데이터를 찾을 수 있습니다.

## <a name="by-file-type"></a>파일 형식별
파일 형식으로 보고서 hello 있습니다 tooview hello 수요와 hello 트래픽 양이 파일 형식 발생 수 있습니다. 이러한 종류의 보고서를 생성 하면 도넛형 차트는 hello 상위 10 개의 파일 형식에 의해 생성 된 적중 횟수의 hello 백분율을 나타냅니다.

> [!TIP]
> Hello 도넛형 차트의 조각 가리키면 hello 인터넷의 미디어 유형 파일 형식을 도구 설명으로 나타납니다.
> 
> 

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 도넛형 차트를 볼 수 있습니다. 있을 것 hello 파일 이름 확장명/인터넷 미디어 유형, hello 총 적중 수, 적중 횟수의 hello 백분율, hello (기가바이트)에 전송 된 데이터 양, hello 각 hello에 대 한 전송 되는 데이터의 백분율 상단 250 파일 형식입니다.

## <a name="by-directory"></a>디렉터리별
hello 디렉터리에서 보고서는 특정 디렉터리의 콘텐츠에 대 한 특정 플랫폼을 통해 발생 되는 수요와 hello 트래픽 tooview hello 양이 있습니다. 이러한 종류의 보고서를 생성 하면 가로 막대형 차트는 hello hello 상위 10 개 디렉터리의 내용에 의해 생성 된 적중 횟수의 총 수를 나타냅니다.

### <a name="using-hello-bar-chart"></a>Hello 가로 막대형 차트를 사용 하 여
* 막대를 위로 마우스를 가져가고 tooview hello 상대 경로 toohello 해당 디렉터리입니다.
* 디렉터리의 하위 폴더에 저장된 콘텐츠는 디렉터리별로 요구량을 계산할 때 포함되지 않습니다. 이 계산 hello hello 실제 디렉터리에 저장 된 콘텐츠에 대해 생성 하는 요청 수에만 전적으로 의존 합니다.
* 이 보고서의 hello 위해서 가장자리 CNAME Url은 변환 된 tootheir 동일한 CDN Url입니다. 이렇게 하면 모든 통계에 대 한 정확한 집계는 자산과 연결 된 hello CDN 또는 가장자리 사용 하는 CNAME URL toorequest에 관계 없이 있습니다.

hello hello 그래프 (y 축)의 왼쪽이 나타냅니다 hello 상위 10 개 디렉터리에 저장 된 hello 콘텐츠에 대 한 요청의 총 수입니다. Hello 차트에서 각 막대는 디렉터리를 나타냅니다. 색 구성표 toomatch 막대를 사용 하 여 hello hello Top 250 전체 디렉터리 섹션에 나열 된 tooa 디렉터리입니다.

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 가로 막대형 차트를 볼 수 있습니다. Hello 다음 각 hello 250 상위 디렉터리에 대 한 정보를 있을 것: 상대 경로, 적중 횟수, 적중 횟수의 hello 백분율, hello 크기 (기가바이트)에서 전송 되는 데이터의 총 hello 및 전송 되는 데이터의 hello 백분율입니다.

## <a name="by-browser"></a>브라우저별
브라우저에서 보고서 hello tooview를 브라우저에서 어떤 된 콘텐츠 사용된 toorequest 있습니다. 이러한 종류의 보고서를 생성 하면 원형 차트는 hello hello 상위 10 개의 브라우저에서 처리 하는 요청의 비율을 나타냅니다.

### <a name="using-hello-pie-chart"></a>Hello 원형 차트를 사용 하 여
* 브라우저의 이름 및 버전의 hello 원형 차트 tooview 조각 마우스로 가리킵니다.
* Hello이이 보고서를 위해 각 고유 브라우저/버전 조합에는 다른 브라우저를 간주 됩니다.
* hello 조각을 "기타" 라는 다른 모든 브라우저 및 버전에 의해 처리 요청의 hello 백분율을 나타냅니다.

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 원형 차트를 볼 수 있습니다. 있습니다 hello 총 적중 수 및 각 hello 상위 250 브라우저에 대 한 적중 횟수의 hello 백분율 hello 브라우저 형식/버전 번호를 찾을 수 있습니다.

## <a name="by-referrer"></a>참조 페이지별
hello에서 Referrer 보고서 hello 선택한 플랫폼에서 tooview hello 상위 참조 페이지 toocontent를 허용 합니다. 참조 페이지 요청을 만든 hello 호스트 이름을 나타냅니다. 이러한 종류의 보고서를 생성 하면 가로 막대형 차트는 hello 상위 10 명의 참조 페이지에 의해 생성 된 요청 (예: 적중) hello 양을 나타냅니다.

hello 그래프 (y 축)의 왼쪽 hello hello 총 자산에 대 한 각 참조 페이지 발생 했음을 요청 수를 나타냅니다. Hello 차트에서 각 막대는 참조 페이지를 나타냅니다. 색 구성표 toomatch 막대를 사용 하 여 hello hello 250 참조 페이지 위쪽 섹션에 나열 된 tooa 참조 페이지입니다.

그 아래 hello 했던 데이터를 사용 하는 toogenerate hello 가로 막대형 차트를 볼 수 있습니다. 있습니다 hello URL, hello 방문 횟수, 총 수 및 각 hello 상위 250 참조 페이지에서 생성 하는 적중 횟수의 hello 백분율을 찾을 수 있습니다.

## <a name="by-download"></a>다운로드별
보고서 다운로드 하 여 hello 가장 많이 요청 된 콘텐츠에 대 한 다운로드 패턴을 tooanalyze 있습니다. hello 보고서의 상단 hello hello에 대 한 완료 된 다운로드를 시도 하는 비교 다운로드 상위 10 개의 요청 된 자산의 가로 막대형 차트를 포함 합니다. 각 막대에 시도 된 다운로드 (파란색) 또는 완료 된 다운로드 (녹색)는 toowhether에 따라 색이 지정 됩니다.

> [!NOTE]
> 이 보고서의 hello 위해서 가장자리 CNAME Url은 변환 된 tootheir 동일한 CDN Url입니다. 이렇게 하면 모든 통계에 대 한 정확한 집계는 자산과 연결 된 hello CDN 또는 가장자리 사용 하는 CNAME URL toorequest에 관계 없이 있습니다.
> 
> 

hello hello 그래프 (y 축)의 왼쪽에는 각각 hello 상위 10 개의 요청 된 자산에 대 한 hello 파일 이름을 나타냅니다. Hello 그래프 (x 축) 바로 아래 해당 hello 다운로드 시도/완료 된 총 수를 나타내는 레이블을 찾을 수 있습니다.

직접 hello 가로 막대형 차트 아래의 다음 정보는 hello 나열 됩니다 hello 상위 250 요청 된 자산에 대 한: 상대 경로 (파일 이름 포함), hello 횟수를 다운로드 한 toocompletion, hello 노드의 수가 요청 된 것 이며 hello 전체 다운로드에 발생 한 요청을의 비율입니다.

> [!TIP]
> 자산이 완전히 다운로드된 경우 CDN은 HTTP 클라이언트(예: 브라우저)에 의해 알려지지 않습니다. 결과적으로, 여부에 따라 toostatus 코드 및 바이트 범위 요청 자산 완전히 다운로드 된 toocalculate를 해야 합니다. hello 먼저 찾을 있습니다 hello 요청 하면 200 OK 상태 코드가 여부는이 계산을 수행 하는 경우. 이 경우 다음 살펴봅니다 바이트 범위 요청 tooensure hello 전체 자산을 처리 하기. 마지막으로 hello hello 요청 된 자산의 toohello 크기 전송 되는 데이터 양을 비교 합니다. Hello 데이터를 전송 하는 경우 같은 tooor hello 파일 크기 보다 크면 하 고 hello 바이트 범위 요청 해당 자산에 대 한 적절 한 hello 적중 전체 다운로드로 계산 됩니다.
> 
> 이 보고서에서는 해석 이기 toohello 인해 유의 hello hello 일관성과이 보고서의 정확도 변경할 수 있는 지점 뒤에 유지 해야 합니다.
> 
> * 사용자 에이전트가 다르게 동작하는 경우 트래픽 패턴을 정확하게 예측할 수 없습니다. 따라서 100%를 초과하는 완료된 다운로드 결과를 생성할 수 있습니다.
> * HTTP 점진적 다운로드를 활용하는 자산은 이 보고서에서 정확하게 표현되지 않을 수 있습니다. 비디오의 toousers 검색 toodifferent 위치 때문입니다.
> 
> 

## <a name="by-404-errors"></a>404 오류별
hello 404 오류 하 여 보고서 tooidentify hello 유형을 hello 404 찾을 수 없음 상태 코드의 대부분의 숫자를 생성 하는 콘텐츠 있습니다. hello 보고서의 상단 hello를 404 찾을 수 없음 상태 코드가 반환 된 hello 상위 10 개의 자산에 대 한 가로 막대형 차트를 포함 합니다. 이 막대형 차트는 hello 총 이러한 자산에 대 한 404 찾을 수 없음 상태 코드가 발생 하는 요청 된 요청 수를 비교 합니다. 각 막대는 색으로 지정됩니다. 노란색 막대는 요청 hello tooindicate 404 찾을 수 없음 상태 코드가 발생 했습니다. 빨강 막대는 tooindicate hello 총 hello 자산에 대 한 요청 수입니다.

> [!NOTE]
> 이 보고서의 hello 위해서 hello 다음 note:
> 
> * 적중 항목은 상태 코드에 관계 없이 자산에 대한 모든 요청을 나타냅니다.
> * 가장자리 CNAME Url은 변환 된 tootheir 동일한 CDN Url입니다. 이렇게 하면 모든 통계에 대 한 정확한 집계는 자산과 연결 된 hello CDN 또는 가장자리 사용 하는 CNAME URL toorequest에 관계 없이 있습니다.
> 
> 

hello hello 그래프 (y 축)의 왼쪽에는 각각 hello 상위 10 개의 요청 된 자산의 404 찾을 수 없음 상태 코드가 발생 하는 hello 파일 이름을 나타냅니다. Hello 그래프 (x 축) 바로 아래 hello 총 요청 수 및 hello 404 찾을 수 없음 상태 코드가 발생 하는 요청 수를 나타내는 레이블을 찾을 수 있습니다.

직접 hello 가로 막대형 차트 아래의 다음 정보는 hello 나열 됩니다 hello 상위 250 요청 된 자산에 대 한: 상대 경로 (파일 이름 포함), 404 찾을 수 없음 상태 코드가 발생, hello 총 횟수를 자산 hello 요청 수가 hello 되었습니다 요청 하 고 hello 404 찾을 수 없음 상태 코드가 발생 하는 요청의 비율입니다.

## <a name="see-also"></a>참고 항목
* [Azure CDN 개요](cdn-overview.md)
* [Microsoft Azure CDN의 실시간 통계](cdn-real-time-stats.md)
* [Hello 규칙 엔진을 사용 하 여 기본 HTTP 동작 재정의](cdn-rules-engine.md)
* [에지 성능 분석](cdn-edge-performance.md)

