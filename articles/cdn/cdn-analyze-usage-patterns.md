---
title: "Azure CDN 사용 패턴 aaaAnalyze | Microsoft Docs"
description: "보고서를 다음 hello를 사용 하 여 CDN에 대 한 사용 패턴을 볼 수 있습니다: 대역폭, 데이터 전송, 적중 횟수, 캐시 상태, Cache Hit Ratio, IPV4/IPV6 데이터 전송 합니다."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d27e6f60acaed66abb27d860c3a3e2e81c9f60cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Azure CDN 사용 패턴 분석

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

아래의 가이드 내용 hello Verizon 프로필에 대 한 hello 관리 포털을 통해 hello 단계 tooview hello 코어 보고서를 통해 이동합니다. 분석 데이터 toostorage 코어, 이벤트 허브 또는 Verizon와 Akamai 프로필에 대 한 로그 분석 (oms)를 내보낼 수 있습니다 [hello azure 포털을 통해](cdn-log-analysis.md)합니다.

보고서를 다음 hello를 사용 하 여 CDN에 대 한 사용 패턴을 볼 수 있습니다.

* 대역폭
* 전송되는 데이터
* 적중 횟수
* 캐시 상태
* 캐시 적중률
* 전송되는 IPv4/IPv6 데이터

## <a name="accessing-core-reports"></a>핵심 보고서 액세스
1. Hello CDN 프로필 블레이드에서 hello 클릭 **관리** 단추입니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-reports/cdn-manage-btn.png)
   
    hello CDN 관리 포털이 열립니다.
2. 마우스 포인터를 놓고 hello **분석** 누른 마우스 포인터를 놓고 hello **코어 보고서** 플라이 아웃입니다.  Hello 메뉴에서 원하는 hello 보고서를 클릭 합니다.
   
    ![CDN 관리 포털 - 핵심 보고서 메뉴](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>대역폭
hello 대역폭 보고서는 특정 기간 동안 HTTP 및 HTTPS에 대 한 hello 대역폭 사용을 나타내는 그래프 및 데이터 테이블의 구성 됩니다. 팝 하는 모든 CDN 또는 특정 POP hello 대역폭 사용량을 볼 수 있습니다. 이 배포와 있습니다 tooview hello 트래픽 급증 Mbps 단위로 팝 하는 CDN에서에 있습니다.

* 모든 노드의 모든 가장자리 노드 toosee 트래픽을 선택 하거나 hello 드롭다운 목록에서 특정 지역/노드를 선택 합니다.
* / 이번 달 오늘/이번 주에 대 한 날짜 범위 tooview 데이터 등를 선택 또는 사용자 지정 날짜를 입력 하 고 선택 사항을 업데이트 되었는지에 toomake "go"를 클릭 합니다.
* 내보낼 수 있습니다 및 hello를 클릭 하 여 hello 데이터 다운로드 excel 시트 아이콘 옆에 있는 너무 "go"입니다.

hello 보고서에는 5 분 마다 업데이트 됩니다.

![대역폭 보고서](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>전송되는 데이터
이 보고서는 특정 기간 동안 HTTP 및 HTTPS에 대 한 hello 트래픽 사용량을 나타내는 그래프 및 데이터 테이블의 구성 됩니다. 팝 하는 모든 CDN 또는 특정 POP hello 트래픽 사용량을 볼 수 있습니다. 이 배포와 있습니다 tooview hello 트래픽 급증 gb에서 팝 하는 CDN에서에 있습니다.

* 모든 메모 toosee 트래픽을 모든 가장자리 노드를 선택 하거나 특정 지역/노드 hello 드롭다운 목록에서 합니다.
* / 이번 달 오늘/이번 주에 대 한 날짜 범위 tooview 데이터 등를 선택 또는 사용자 지정 날짜를 입력 하 고 선택 사항을 업데이트 되었는지에 toomake "go"를 클릭 합니다.
* 내보낼 수 있습니다 및 hello를 클릭 하 여 hello 데이터 다운로드 excel 시트 아이콘 옆에 있는 너무 "go"입니다.

hello 보고서에는 5 분 마다 업데이트 됩니다.

![전송되는 데이터 보고서](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>적중 횟수(상태 코드)
이 보고서는 콘텐츠에 대 한 요청 상태 코드의 hello 분포를 설명합니다. 각 콘텐츠 요청에서 HTTP 상태 코드가 생성됩니다. hello 상태 코드 가장자리 Pop hello 요청을 처리 하는 방법을 설명 합니다. 예를 들어 2xx 상태 코드가 4xx 상태 코드 이면 오류가 발생 했습니다 해당 hello 요청이 tooa 클라이언트를 성공적으로 처리 된 나타냅니다. HTTP 상태 코드에 대한 자세한 내용은 [상태 코드](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)를 참조하세요.

* / 이번 달 오늘/이번 주에 대 한 날짜 범위 tooview 데이터 등를 선택 또는 사용자 지정 날짜를 입력 하 고 선택 사항을 업데이트 되었는지에 toomake "go"를 클릭 합니다.
* 내보낼 수 있습니다 및 hello를 클릭 하 여 hello 데이터 다운로드 excel 시트 옆에 있는 너무 "go"입니다.

![적중 횟수 보고서](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>캐시 상태
이 보고서는 캐시 적중 횟수와 클라이언트 요청에 대 한 캐시 누락 수의 hello 분포를 설명합니다. Hello 보다 빠른 성능을 캐시 적중 횟수에 도달할 이후 만료 된 캐시 적중 수 및 캐시 누락 수를 최소화 하 여 데이터 배달 속도 최적화할 수 있습니다. "캐시" 응답 헤더를 할당 하 여 원본 서버 tooavoid를 구성 하 여, 꼭 필요한 경우를 제외 하 고 쿼리 문자열 캐싱을 사용 하지 않음으로써 및 캐시할 응답 코드를 방지 하 여 캐시 누락 수를 줄일 수 있습니다. 만료 캐시 적중 가능한 toominimize hello toohello 원본 서버에 요청 수가으로 자산 최대 처리 기간을 늘리면 방지할 수 있습니다.

![캐시 상태 보고서](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>기본 캐시 상태는 다음과 같습니다.
* TCP_HIT: 에지에서 처리됩니다. hello 개체가 캐시에 있으며 해당 최대 처리 기간을 초과 했습니다.
* TCP_MISS: 원본에서 처리됩니다. hello 응답이 백 tooorigin를 hello 개체가 캐시에 없어서 합니다.
* TCP_EXPIRED _MISS: 원본을 사용하여 유효성을 재검사한 후 원본에서 처리됩니다. hello 개체가 캐시에 했지만 해당 최대 처리 기간을 초과 했습니다. Origin와 유효성 재검사 원본에서 새 응답 대체 되 고 hello 캐시 개체에서 발생 했습니다.
* TCP_EXPIRED _HIT: 원본을 사용하여 유효성을 재검사한 후 에지에서 처리됩니다. hello 개체가 캐시에 했지만 해당 최대 처리 기간을 초과 했습니다. Hello 원본 서버와 유효성 재검사 되 고 수정 되지 않은 hello 캐시 개체에서 발생 했습니다.
* / 이번 달 오늘/이번 주에 대 한 날짜 범위 tooview 데이터 등를 선택 또는 사용자 지정 날짜를 입력 하 고 선택 사항을 업데이트 되었는지에 toomake "go"를 클릭 합니다.
* 내보낼 수 있습니다 및 hello를 클릭 하 여 hello 데이터 다운로드 excel 시트 아이콘 옆에 있는 너무 "go"입니다.

### <a name="full-list-of-cache-statuses"></a>캐시 상태 전체 목록
* TCP_HIT-hello POP toohello 클라이언트에서 직접 요청을 서비스 하는 경우이 상태가 보고 됩니다. 자산은 hello POP 가장 가까운 toohello 클라이언트에서 캐시 되 고 있기 유효한-time-to-live, POP 또는 TTL 서비스 즉시 됩니다. TTL는 hello 응답 헤더 다음에 의해 결정 됩니다.
  
  * Cache-Control: s-maxage
  * Cache-Control: max-age
  * 만료
* TCP_MISS-이 상태 hello POP 가장 가까운 toohello 클라이언트 hello 요청 된 자산의 캐시 된 버전을 찾을 수 없음을 나타냅니다. hello 자산 원본 서버 또는 원본 방패 서버에서 요청 됩니다. Hello 원본 서버 또는 hello 원본 방패 서버 자산을 반환할 경우 되 toohello 클라이언트 served 고 hello 클라이언트와 hello에 지 서버에 캐시 합니다. 그렇지 않으면 200 이외의 상태 코드(예: 403 사용할 수 없음, 404 찾을 수 없음 등)가 반환됩니다.
* TCP_EXPIRED _HIT-hello POP toohello 클라이언트에서 직접 TTL이 만료 된, hello 자산 최대 처리 기간 만료 된 시점와 같은 자산을 대상으로 하는 요청을 처리 하는 경우이 상태가 보고 됩니다.
  
    유효성 재검사 요청 toohello 원본 서버는 만료 된 요청 일반적으로 발생합니다. TCP_EXPIRED _HIT toooccur에 대 한 순서로 hello 원본 서버는 최신 버전의 hello 자산 존재 하지 않는 지정 해야 합니다. 이러한 상황에서는 일반적으로 해당 자산의 Cache-Control 및 Expires 헤더가 업데이트됩니다.
* TCP_EXPIRED _MISS-hello POP toohello 클라이언트에서 최신 버전의 만료 된 캐시 된 자산 제공 될 때이 상태가 보고 됩니다. 이 캐시 된 자산에 대 한 hello TTL 만료 될 때 발생 (예: 만료 되는 최대 처리 기간) hello 원본 서버에 해당 자산의 최신 버전을 반환 합니다. 이 새로운 버전의 hello 자산은 hello 캐시 된 버전 대신 toohello 클라이언트를 처리 됩니다. 또한에 지 서버 hello와 hello 클라이언트에 캐시 됩니다.
* CONFIG_NOCACHE-이 상태 우리의 가장자리 POP에 고객 관련 구성을 캐시할 hello 자산 수를 나타냅니다.
* NONE - 이 상태는 캐시 콘텐츠 새로 고침 검사가 수행되지 않았음을 나타냅니다.
* TCP_ CLIENT_REFRESH _MISS-HTTP 클라이언트 (예: 브라우저) hello 원본 서버에서 가장자리 POP tooretrieve 새 버전의 오래 된 자산을 강제로 수행 하는 경우이 상태가 보고 됩니다.
  
    기본적으로 서버는 HTTP 클라이언트 hello 원본 서버에서 새 버전의 hello 자산 우리의 edge 서버 tooretrieve을 강제할 수 없도록 방지 합니다.
* TCP_ PARTIAL_HIT - 바이트 범위 요청에 의해 부분적으로 캐시된 자산이 적중되는 경우 이 상태가 보고됩니다. hello 요청 바이트 범위는 즉시 hello POP toohello 클라이언트에서 제공 됩니다.
* UNCACHEABLE-자산 캐시 제어 및 Expires 헤더는 해당 캐시 되어서는 안 또는 hello HTTP 클라이언트를 POP에 나타낼 때이 상태가 보고 됩니다. 이러한 종류의 요청 hello 원본 서버에서 처리 되므로

## <a name="cache-hit-ratio"></a>캐시 적중률
이 보고서는 캐시에서 직접 처리 된 캐시 된 요청의 hello 비율을 나타냅니다.

hello 보고서 hello를 다음 세부 정보를 제공 합니다.

* hello는 hello POP 가장 가까운 toohello 요청자에 캐시 된 콘텐츠를 요청 했습니다.
* 이것이 네트워크 hello 가장자리에서 직접 hello 요청을 처리 합니다.
* hello 요청 hello 원본 서버와 유효성 재검사가 필요 하지 않습니다.

hello 보고서에 포함 되지 않습니다.

* 필터링 옵션 toocountry 인해 거부 된 요청 수입니다.
* 헤더에 캐시하지 않도록 표시된 자산에 대한 요청 예를 들어 Cache-Control: private, Cache-Control: no-cache 또는 Pragma: no-cache 헤더는 자산이 캐시되지 않도록 합니다.
* 부분적으로 캐시된 콘텐츠에 대한 바이트 범위 요청.

hello 공식은: (TCP_ 적중 / (TCP_ 적중 + TCP_MISS)) * 100

* / 이번 달 오늘/이번 주에 대 한 날짜 범위 tooview 데이터 등를 선택 또는 사용자 지정 날짜를 입력 하 고 선택 사항을 업데이트 되었는지에 toomake "go"를 클릭 합니다.
* 내보낼 수 있습니다 및 hello를 클릭 하 여 hello 데이터 다운로드 excel 시트 아이콘 옆에 있는 너무 "go"입니다.

![캐시 적중률 보고서](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>전송되는 IPv4/IPv6 데이터
이 보고서는 IPV4 및 i p v 6의 hello 트래픽 사용 분포를 표시합니다.

![전송되는 IPv4/IPv6 데이터](./media/cdn-reports/cdn-ipv4-ipv6.png)

* / 이번 달 오늘/이번 주에 대 한 날짜 범위 tooview 데이터 등을 선택 하거나 사용자 지정 날짜를 입력.
* 그런 다음 선택 사항을 업데이트 되었는지에 toomake "go"를 클릭 합니다.

## <a name="considerations"></a>고려 사항
보고서만 생성할 수 있습니다 hello 내에서 마지막 18 개월입니다.

